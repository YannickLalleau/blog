# Prestashop : Ajouter le support de la prise en compte du format webp dans l'ajout de visuel produit

Une fonctionnalité prévue sur la version 1.9 en attendant, il faut bricoler pour cela nous allons utiliser le commit suivant :
https://github.com/PrestaShop/PrestaShop/pull/24394/commits/377418418ed9ae902332c856bc688e2f85506405

Le principe c'est de pouvoir ajouter des visuels produits au format webp. Ici on ne traite pas la possibilité de pouvoir
générer des visuels au format webp

Manipulation réalisation sur la version de PrestaShop : 1.7.8.7

Modifier les fichiers suivants :

```
- **/controllers/admin/AdminProductsController.php:2819**  
  Avant :  
  $image_uploader->setAcceptTypes(['jpeg', 'gif', 'png', 'jpg'])->setMaxSize($this->max_image_size);  
  Après :   
  $image_uploader->setAcceptTypes(['jpeg', 'jfif', 'gif', 'png', 'webp'])->setMaxSize($this->max_image_size);
```
```
- **/classes/ImageManager.php:448**
    - Avant :  
      $authorizedExtensions = ['gif', 'jpg', 'jpeg', 'jpe', 'png'];
    - Après :  
      $authorizedExtensions = ['gif', 'jpg', 'jpeg', 'jpe', 'png', 'webp'];
```
```
- **/classes/ImageManager.php:42**
'image/jpeg',
'image/pjpeg',
'image/png',
-        'image/x-png',
+        'image/x-png',
+        'image/webp',
  ];
```
```
- **/classes/ImageManager.php:42**
  case IMAGETYPE_PNG:
  return imagecreatefrompng($filename);

-                break;
+               break;
+
+            case IMAGETYPE_WEBP:
+               return imagecreatefromwebp($filename);

             case IMAGETYPE_JPEG:
             default:
```