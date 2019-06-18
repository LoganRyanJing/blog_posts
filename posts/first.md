---
title: "First"
date: 2019-06-18T09:42:51+08:00
draft: false
---

### WordPress查找主图（ featured image）
* 数据库查询
```mysql
    SELECT p.* FROM wp_postmeta AS pm 
        INNER JOIN wp_posts AS p 
        ON pm.meta_value=p.ID 
        WHERE pm.post_id = $da_id 
        AND pm.meta_key = '_thumbnail_id' 
        ORDER BY p.post_date DESC 
        LIMIT 15; 
```
---
> #### Wp关联查询主图以及作者
```
SELECT p.*,( SELECT guid FROM wp_posts WHERE id = m.meta_value ) AS imgurl, (SELECT meta_value FROM wp_postmeta pm WHERE meta_key='_wp_attachment_metadata' AND pm.post_id=m.meta_value ) AS imgdetails,pus.`display_name`
FROM wp_posts p
LEFT JOIN  wp_postmeta m ON(p.id = m.post_id AND m.meta_key =  '_thumbnail_id' )
LEFT JOIN  wp_users AS pus ON p.post_author=pus.id
WHERE p.post_type =  'post'
AND p.post_status =  'publish';
```

