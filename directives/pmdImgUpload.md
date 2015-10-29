# Pmd Img Upload

## ::pmdImgUpload  
#### Module Name
common.imgUpload

#### 參數說明
* imageData: 為一個 image data 的 object
* imageData.images: 圖片資訊的陣列，從DB撈出來的資料
* imageData.imagesResult: 選擇的圖片, 單一值
* imageUploadFn: 上傳圖片的 function, 最後要回傳一個 callback
* deleteImageFn: 刪除圖片的 function, 最後要回傳一個 callback
* SelectedFn: 選擇圖片後的 function, 最後要回傳一個 callback
 
#### 使用範例
```
    $scope.imgUploadConfig =
      imageData:
        images: []
        imagesResult: {}

    $sails.get("/image/index").success (data) ->
      $scope.adImages = data.adImages
      $scope.imgUploadConfig.imageData.images = _.map data.adImages, (value, key)->
        value.imgBase64 = value.previewImageBase64
        return value
      return

    $scope.imageUploadFn = (file, busy)->
      Upload.upload(
        url: '/image/create'
        file: file
      ).success (data, status, headers, config) ->
        busy("false")
    
    $scope.deleteImageFn = (hash, next)->
      $sails.post("/image/delete", {hash: hash}).success (data)->
        success = if data.type is "danger" then false else true
        return next success
    
    $scope.selectedFn = (image, next)->
      next true
```
```
img-upload(image-data="imgUploadConfig.imageData" image-upload-fn="imageUploadFn" delete-image-fn="deleteImageFn" selected-fn="selectedFn")
```

::搭配 mk-modal

```
# mk-model
    $scope.modalConfig =
      zIndex: 10
      effect: "mkmd-effect-susab"
      style:
        height: '97%'
        width: "100%"
    $scope.openUploadModal = ->
      $("#uploadModalTriggerBtn").click()
      return
    $scope.closeModal = ->
      $('#uploadModalCloseBtn').click()
      return

    $scope.afterCloseHandler = ->
      console.log "afterCloseHandler"

    $scope.beforeCloseHandler = ->
      console.log "beforeCloseHandler"
      
    $scope.changeLibrary = (target)->
      $scope.selectLibrary = target
# img upload
     $scope.imgUploadConfig =
      imageData:
        images: []
        imagesResult: {}

    $sails.get("/image/index").success (data) ->
      $scope.adImages = data.adImages
      $scope.imgUploadConfig.imageData.images = _.map data.adImages, (value, key)->
        value.imgBase64 = value.previewImageBase64
        return value
      return

    $scope.imageUploadFn = (file, busy)->
      Upload.upload(
        url: '/image/create'
        file: file
      ).success (data, status, headers, config) ->
        busy("false")
    
    $scope.deleteImageFn = (hash, next)->
      $sails.post("/image/delete", {hash: hash}).success (data)->
        success = if data.type is "danger" then false else true
        return next success
    
    $scope.selectedFn = (image, next)->
      next true
```

```
    button.btn(ng-click="openUploadModal()")
      | open
    button#uploadModalTriggerBtn.hide uploadModalTriggerBtn
    button#uploadModalCloseBtn.hide uploadModalCloseBtn
    mk-modal(mk-modal-id="mk-upload", trigger-element-id="uploadModalTriggerBtn",
      close-element-id="uploadModalCloseBtn", data="modalConfig",
      after-close="afterCloseHandler()", before-close="beforeCloseHandler()", before-open="beforeOpen(imgUploadConfig)")
      .modal-container
        #mk-navbar.mkmd-title
          .navbar-left
            ul.pull-left.preview-type-group
              li
                a.nav-targe(ng-click="changeLibrary('img')" ng-class="{ active: selectLibrary === 'img' }")
                  | {{ "upload-img-library" | translate }}
              li
                a.nav-targe(ng-click="changeLibrary('video')" ng-class="{ active: selectLibrary === 'video' }")
                  | {{ "upload-video-library" | translate }}
          .navbar-right
            i.fa.fa-times(ng-click="closeModal()")

        #mk-preview-wrap
          img-upload(image-data="imgUploadConfig.imageData" image-upload-fn="imageUploadFn" delete-image-fn="deleteImageFn" selected-fn="selectedFn")

```

  
