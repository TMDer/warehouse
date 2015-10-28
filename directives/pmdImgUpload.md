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
    $scope.creativeImages = []
    $scope.imagesResult = {}
    $scope.imageUploadFn = (file, busy)->
      // do...
      Upload.upload(
        url: '/image/create'
        file: file
      ).success (data, status, headers, config) ->
        busy("false")
        
    $scope.deleteImageFn = (hash, next)->
      // do...
      $sails.post("/image/delete", {hash: hash}).success (data)->
        success = if data.type is "danger" then false else true
        return next success 
    $scope.selectedFn = (image, next)->
      // do...
      next true
```
```
img-upload(images="creativeImages" image-upload-fn="imageUploadFn" images-result="imagesResult" delete-image-fn="deleteImageFn" selected-fn="selectedFn")
```
   
  
