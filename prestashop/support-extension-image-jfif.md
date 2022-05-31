# Prestashop : Ajouter le support de l'extension image Jfif / Jpeg dans les images de produit

Manipulation réalisation sur la version de PrestaShop : 1.7.8.5

Modifier les fichiers suivants :

- **/controllers/admin/AdminProductsController.php:2819**  
  Avant :  
  $image_uploader->setAcceptTypes(['jpeg', 'gif', 'png', 'jpg'])->setMaxSize($this->max_image_size);  
  Après :   
  $image_uploader->setAcceptTypes(['jpeg', 'jfif', 'gif', 'png', 'jpg'])->setMaxSize($this->max_image_size);
- **/classes/ImageManager.php:448**
    - Avant :  
      $authorizedExtensions = ['gif', 'jpg', 'jpeg', 'jpe', 'png'];
    - Après :  
      $authorizedExtensions = ['gif', 'jpg', 'jpeg', 'jpe', 'png', 'jfif'];

