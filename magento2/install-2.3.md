# Instalación Magento 2.3 - Windows

### Adicionalmente, crear tema y establecer gulp para desarrollo con livereload (yay!)

1. Crear proyecto:

    ```bash
    composer create-project --repository=https://repo.magento.com/ magento/project-community-edition magento2
    ```

2. Parchear magento:

    ```Magento\Framework\View\Element\Template\File\Validator.php```

    ```php
    //$realPath = $this->fileDriver->getRealPath($path);
    $realPath = str_replace('\\', '/', $this->fileDriver->getRealPath($path));    //EH0219
    ```

3. Eliminar archivos innecesarios.

4. Excluir var y pub.

5. Añadir xsl schemas:

    ```bash
    php bin/magento dev:urn-catalog:generate .idea/misc.xml
    ```

6. Instalar español (opcional):

    https://github.com/mageplaza/magento-2-spanish-language-pack

7. Instalar gulp:

    https://github.com/subodha/magento-2-gulp
    
    Usar los archivos que hay en la carpeta "gulp" que están ligeramente modificados, 
    actualizando gulp a la versión 4.0 y cambiando el watcher para los archivos de app
    ya que los de pub me estaban haciendo trigger de livereload constantemente.

    Instalar LiveReload.

8. Crear tema (test):

   * Crear carpeta dentro de app/design/frontend/Vendor/theme
   * Crear registration.php
   * Crear theme.xml
   * Establecer tema en magento2: Content > Design > Configuration

8. Testear:

   * Crear web/css/source/_extend.less
   * Añadir algo de código css de prueba.
   
> NOTA
>
> Si añades un fichero nuevo css/js, hay que hacer lo siguiente:
>
> * rm -rf pub/static/frontend/{Vendor}/{theme}/{locale}
> * php bin/magento cache:clean
> * gulp exec --theme
> * gulp watch --theme --live
>
> Si no, no verás los cambios.
