
Create a connection between the software and the displays : with mlx_init

    mlx_new_window      : manage windows
    mlx_pixel_put       : draw inside window
    mlx_new_image       : manipulate images
     mlx_loop            : handle keyboard or mouse events


After getting the image address the bytes are not aligned this means that the size_line differ from the actual window width. Therefore should ALWAYS calculate the memory offset using the size lien set by `mlx_get_data_addr`
Formula of offset : `(y * line_length + x * (bits_per_pixel / 8));`

