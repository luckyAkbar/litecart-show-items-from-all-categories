

████████ ███████  ██████ ██   ██ ███    ██  ██████  
   ██    ██      ██      ██   ██ ████   ██ ██    ██ 
   ██    █████   ██      ███████ ██ ██  ██ ██    ██ 
   ██    ██      ██      ██   ██ ██  ██ ██ ██    ██ 
   ██    ███████  ██████ ██   ██ ██   ████  ██████  
      [store.0ad.xyz](https://store.0ad.xyz)           
                                                    
███████ ████████  ██████  ██████  ███████           
██         ██    ██    ██ ██   ██ ██                
███████    ██    ██    ██ ██████  █████             
     ██    ██    ██    ██ ██   ██ ██                
███████    ██     ██████  ██   ██ ███████           
        
                                                    
                                                                                     
# Show Items on Every Categories
## A LiteCart Addons
This addon will display listings from items on each category in your index page, so customers can see all of them!

## What does this addon do?
This addon will insert a new box just below the default listings for litecart's Latest Product for each categories you have in your store. You can also control how much items per category to be shown.

## What's inside this addon
Inside this addon, you will find three files: one vmod file to make the virtual changes necessary to inject this feature into your index page, a view file containing HTML as a template for item boxes of each category, and lastly, a boxes file that contains the logic behind this feature, such as fetching data and rendering the page.

## Known Issue
Before proceeding further, I need to tell you that there is one issue regarding this addon. Don't worry, it is not a bug, rather it is an added technical difficulty you have to endure because of the vmod ``` <install></install> ``` and ``` <uninstall></uninstall> ``` feature is not working. <br>
If you see the [litecart's vmod wiki](https://www.litecart.net/en/wiki/how_to_create_a_vmod), inside the ``` <install></install> ``` and ``` <uninstall></uninstall> ``` can be filled with PHP code that runs during install and uninstall process. This addon needs to insert a row to the database table for configuration to make this feature work. Unfortunately, that process cannot be automated. Fortunately, though, that process is simple to do manually, and I will explain it to you in this README file.

## Steps to install
### Prerequisite
1. Always backup data before making changes to your store to avoid data loss / corrupt instalation. Better safe than sorry eventhough the chances are smaller than atom :)
2. Make sure you have access to Mysql database as you will need to execute SQL command
3. Make sure you have access to your server filesystem, especially the litecart instalation

### Steps
1. Get access to all the code in this repository, whether directly from [litecart's addons page](https://link.0ad.xyz/show-items-categories), or clone this github repository
2. Upload all the content of [public_html](./public_html/) to the respective their respective path.
3. Access your sql server, and connect to your litecart's database
4. Copy this sql command. Take a note that you have to change the databse table name to make this script works. However, other values inside the sql VALUE() isn't needed to be changed as you can change it later inside the admin page.
```sql
INSERT INTO CHANGE-THIS-TO-YOUR-DB-TABLE-NAME (
    `setting_group_key`, `type`, `key`,
    `value`, `title`, `description`,
    `function`, `priority`
) VALUES (
    'listings', 'local', 'vmodcfg_scoip_num_items_per_category',
    '10', 'Num Items per Category for Show Categories on Index Page', 'The number of items to be shown per category',
    'number()', 0
);
```
5. Run the sql command
6. Enable the VMod app in admin page
7. You should see a number of items on each category product you have now listed in the index page.

## Steps to uninstall
### Temporary uninstall
If you just want to deactivate this addon, you just need to deactivate the VMod. After that, your product listing on the index page will back previous look
### Permanent uninstall
When you need to get rid of this addon, for whatever reason, you need to follow this steps
1. Disable the vmod from admin page
2. execute this SQL command directly to your litecart's database, remember to change the table name.
```sql
DELETE FROM CHANGE-THIS-TO-YOUR-DB-TABLE-NAME 
WHERE `key` = 'vmodcfg_scoip_num_items_per_category';
```
3. Delete all the respective files in this repository from your litecart's instalation filesystem.