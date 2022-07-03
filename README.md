# RequeestPermission


# 1 Permission READ từ Bộ nhớ máy 


# Step 1 : Tạo RequestCode Image
```
private val IMAGE_REQ = 1
```


# Step 2 : Tạo fun selectImage
```
private fun selectImage() {
        val intent = Intent()
        intent.type = "image/*" // if you want to you can use pdf/gif/video
        intent.action = Intent.ACTION_GET_CONTENT
        someActivityResultLauncher.launch(intent)
}
```


# Step 3.  Sử dụng registerActivityForResult để lấy request code
```
private var someActivityResultLauncher = registerForActivityResult(ActivityResultContracts.StartActivityForResult()) { result ->
        if (result.resultCode == AppCompatActivity.RESULT_OK) {
            val data = result.data
            imagePath = data!!.data
            Picasso.get().load(imagePath).into(binding.civAvatar)
        }

}
```


# Step 4 : Tạo fun requestPermission
```
private fun requestPermission() {
        if (ContextCompat.checkSelfPermission(
                requireActivity(),
                Manifest.permission.READ_EXTERNAL_STORAGE
            )
            == PackageManager.PERMISSION_GRANTED
        ) {
            selectImage()
        } else {
            ActivityCompat.requestPermissions(
                requireActivity(), arrayOf(
                    Manifest.permission.READ_EXTERNAL_STORAGE
                ), IMAGE_REQ
            )
        }
}
```


# 2 Permission Camera

# Step 1 : Tạo RequestCode Image
```
private val IMAGE_REQ = 1
```


# Step 2 : Tạo fun accessCamera để truy cập vào camera
```
private fun accessCamera() {
        val intent = Intent()
       
        intent.action = android.provider.MediaStore.ACTION_IMAGE_CAPTURE
        someActivityResultLauncher.launch(intent)
}
```


# Step 3.  Sử dụng registerActivityForResult để lấy request code
```
private var someActivityResultLauncher = registerForActivityResult(ActivityResultContracts.StartActivityForResult()) { result ->
        if (result.resultCode == AppCompatActivity.RESULT_OK) {
            val data = result.data
            imagePath = data!!.data
            Picasso.get().load(imagePath).into(binding.civAvatar)
        }

}
```


# Step 4 : Tạo fun requestPermission
```
private fun requestPermission() {
        if (ContextCompat.checkSelfPermission(
                requireActivity(),
                Manifest.permission.CAMERA
            )
            == PackageManager.PERMISSION_GRANTED
        ) {
            accessCamera()
        } else {
            ActivityCompat.requestPermissions(
                requireActivity(), arrayOf(
                    Manifest.permission.CAMERA
                ), IMAGE_REQ
            )
        }
}
```
