Hook intercept functions call or messages or events passed between software components.

## key_hook

Mlx function :  `int mlx_key_hook ( void *win_ptr, int (*funct_ptr)(), void *param );`
Logic : When pressed any key it will execute the function passed as arguments. In that function you have to execute code if for exemple you press ESC
Exemple on linux
```c
int ft_close(int keycode, t_data *data)
{
    ft_printf("%d\n",keycode);
    if ( keycode == l_esc)
        mlx_destroy_window(data->mlx,data->window);
   return(0);
}
```

