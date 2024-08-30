---
title: Admin UI Translation
description: Having a multi-language admin
weight: 100
layout: docs
---

# Admin Multi-Language Support
**Prior to v2.1.0 very little of the Admin Interface would "display" in a language other than English.**

**Admin Configuration Menu Translations**
Since v1.5.5 it was possible to define translations in language packs for the Admin "Configuration" menu
using a few override conventions:
```
//For example, in admin/includes/languages/spanish/lang.configuration.php

define('CFGTITLE_STORE_NAME', 'Nombre de la Tienda');
define('CFGDESC_STORE_NAME', 'El nombre de mi tienda');
define('CFG_GRP_TITLE_MY_STORE', 'Mi Tienda');
```

### Now with v2.1.0 this is expanded to more areas:

**For product_types:**

The `product_type` `type_name` can be defined using 
`'PRODUCT_TYPE_NAME_FOR_HANDLER_'` followed by the product_type's uppercase `type_name`

**Example for French:**
```
    'PRODUCT_TYPE_NAME_FOR_HANDLER_PRODUCT' => 'Produit - Général',
    'PRODUCT_TYPE_NAME_FOR_HANDLER_PRODUCT_MUSIC' => 'Produit - Musique',
    'PRODUCT_TYPE_NAME_FOR_HANDLER_DOCUMENT_GENERAL' => 'Document - Général',
    'PRODUCT_TYPE_NAME_FOR_HANDLER_DOCUMENT_PRODUCT' => 'Document - Produit',
    'PRODUCT_TYPE_NAME_FOR_HANDLER_PRODUCT_FREE_SHIPPING' => 'Produit - Envoi Gratuit',
```

**And for Product Type layout/configuration settings** (found in product_type_layout table's configuration_title and configuration_description fields):
`'PRODUCT_TYPE_LAYOUT_TITLE_FOR_'` followed by uppercase `configuration_key`
`'PRODUCT_TYPE_LAYOUT_DESC_FOR_'` followed by uppercase `configuration_key`

French examples:
```
    'PRODUCT_TYPE_LAYOUT_TITLE_FOR_SHOW_PRODUCT_INFO_MODEL' => 'Afficher le modèle',
    'PRODUCT_TYPE_LAYOUT_DESC_FOR_SHOW_PRODUCT_INFO_MODEL' => 'Afficher le numéro de modèle dans les informations de produit 0= off 1= on',
    'PRODUCT_TYPE_LAYOUT_TITLE_FOR_SHOW_PRODUCT_INFO_WEIGHT' => 'Afficher le poids',
    'PRODUCT_TYPE_LAYOUT_DESC_FOR_SHOW_PRODUCT_INFO_WEIGHT' => 'Afficher le poids dans les informations de produit 0= off 1= on',
    'PRODUCT_TYPE_LAYOUT_TITLE_FOR_SHOW_PRODUCT_INFO_MANUFACTURER' => 'Afficher le fabricant',
    'PRODUCT_TYPE_LAYOUT_DESC_FOR_SHOW_PRODUCT_INFO_MANUFACTURER' => 'Afficher le nom du fabricant dans les informations de produit 0= off 1= on',
(and there are a few dozen more possible entries that can be translated this way)
```

**For Plugins listed in the Plugin Manager**
In your plugin's language file, add a define:
`'ADMIN_PLUGIN_MANAGER_DESCRIPTION_FOR_'` followed by the uppercase english `Description`

French examples:
```
    'ADMIN_PLUGIN_MANAGER_DESCRIPTION_FOR_DISPLAYLOGS' => 'Affiche et gère les fichiers journaux de Zen Cart.',
    'ADMIN_PLUGIN_MANAGER_DESCRIPTION_FOR_POSM' => 'Ce plugin permet à votre site d\'attribuer des niveaux de stock et des numéros de modèle à vos produits en fonction de combinaisons produit-attributs (également appelées « variantes de produit » ou « stock par attributs »).',
```

## Translations Added When Installing A Language Pack

When a Language is added to the Admin via the Languages page, not only do you specify the "directory name" where the language-pack files are to be found,
but Zen Cart also makes copies of a LOT of database-records to support that language. It copies the English version of products, categories, and other things, and then you are free to edit those names/descriptions to translate them into your other language.

For a few core things like Order Status, since v2.1.0 you can now pre-define a few language-defines that will be used instead of the English default.

**Order Status pre-defined defaults**
Put the following constants into the `admin` `lang.languages.php` or a file in `extra_definitions`

(Example from a French language pack)
```
'INSTALL_ORDER_STATUS_PENDING' => 'En attente',
'INSTALL_ORDER_STATUS_PROCESSING' => 'En cours',
'INSTALL_ORDER_STATUS_DELIVERED' => 'Livré',
'INSTALL_ORDER_STATUS_UPDATE' => 'Mise à jour'
```
Note the pattern: `INSTALL_ORDER_STATUS_` prefix, followed by the uppercase existing English name.

Any statuses for which a matching define is not found, will just use the English value, as before, and can be manually translated via the Admin UI as before.

NOTE: If a language is already-installed, it is best just to fix the value directly using the Admin UI, because language-file constants in these cases are only for when a language is first installed.


**Pre-Defined Values for Plugins**
Encapsulated Plugins, such as POSM, might make similar copies of English values when adding a new language.

**Consult each plugin to determine what constants** can be established as defines that will be read when installing a new language.

NOTE: If a language is already-installed, it is best just to fix the value directly using the Admin UI, because language-file constants in these cases are only for when a language is first installed.