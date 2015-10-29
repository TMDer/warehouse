# Pmd Img Upload

## ::pmdImgUpload  
#### Module Name
common.imgUpload

#### 參數說明
* images: 圖片資訊的陣列，從DB撈出來的資料
* imagesResult: 選擇的圖片, 單一值
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
   

  
