# Content type bypass

In the page '/?page=upload#' we can upload an image but not every extension.
For exemple jpeg and jpg are working but when we try to upload png image we get this "Your image was not uploaded.".

To get the flag I just change try to upload a png image and change the content type of the request by jpeg.
