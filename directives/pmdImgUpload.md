# Pmd Img Upload

## ::pmdImgUpload  
#### Module Name
common.imgUpload

#### 參數說明
* images: 圖片資訊的陣列
* imagesResult: 選擇的圖片
* imageUploadFn: 上傳圖片的 function
* deleteImageFn: 刪除圖片的 function
* SelectedFn: 選擇圖片後的 function
 
#### 使用範例
```
    # mk-model
    $scope.modalConfig =
      zIndex: 10
      effect: "mkmd-effect-susab"
      style:
        height: '97%'
        width: "100%"

    $scope.imgUploadConfig =
      images: {}
      imagesResult: {}

    $sails.get("/image/index").success (data) ->
      $scope.adImages = data.adImages
      $scope.imgUploadConfig.images = _.map data.adImages, (v,i)->
        v.imgBase64 = v.previewImageBase64
        return v
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
```
```
img-upload(images="creativeImages" image-upload-fn="imageUploadFn" images-result="imagesResult" delete-image-fn="deleteImageFn" selected-fn="selectedFn")
```
   
  
