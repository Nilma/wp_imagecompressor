# WordPress Image Compressor Plugin 

### Hooking into the Upload Process

**`add_filter( 'wp_handle_upload', 'mic_compress_uploaded_image' );`**
- Registers our function to run after a file is uploaded.
- Gives us a chance to edit/replace the file before WordPress saves it.

---

### Working with File Paths

**`$upload['file']`**
- Absolute path to uploaded file.
- Used for file system operations (open, edit, delete).

**`pathinfo($file_path, PATHINFO_EXTENSION)`**
- Extracts file extension (`jpg`, `png`, etc.).
- Helps determine how to handle the image.

---

### GD Library Image Functions

**`imagecreatefromjpeg()` / `imagecreatefrompng()` / `imagecreatefromgif()`**
- Load image from file into PHP memory as a GD image resource.

**`imagejpeg($image, $file_path, $quality)`**
- Compress and save the image as JPEG.
- `quality` ranges from 0 (worst) to 100 (best).

**`imagedestroy($image)`**
- Frees up memory used by the image resource.

---

### File Handling

**`unlink($file_path)`**
- Deletes a file from the server.
- Optional: used when converting PNG to JPEG to remove the original.

---

### Updating Return Value to WordPress

**`$upload['file']` / `$upload['url']`**
- Must be updated if filename or extension changes.
- WordPress will use the values we return from the filter.

