# WP-common-vulnearbilities
WordPress common vulnerabilities

### is_admin
`is_admin` simply checks if the page is the current request is for an administrative interface page.

`is_admin` should be accompanied with capability check. 
1. Is the current user viewing an Admin panel? 
2. Is the user authenticated with valid session? 
2. Is the user authorized to view the functions on the Admin panel? 

``````
if ( ! is_admin() ) {
    echo 'This is not an Admin panel.';
} else {
    echo 'You're viewing an Admin panel.';
}
``````

`is_admin` does not have **capability check**. It does not check if the user is an administrator. 


```
// if is_admin() is false, which means if it's not an Admin pnel, then stop executing. 
if (!is_admin()) {
 die();
}
```


```
// If is_admin() is true, in which it's an admin, a function is not required. 
$req = 'required';
  if(is_admin()){
    $req = '';
  }
```

#### Check user capabilities

`is_user_logged_in()`
`user_can( $user, $capability )`


```
if ( ! is_admin() ) {
    wp_die( 'This is not an Admin panel.' );
}

if ( ! is_user_logged_in() ) {
    wp_die( 'You are not logged in.' );
}

if ( ! user_can( $id_user, 'my_capability' ) {
    wp_die( 'You are not an authorized user.' );
}
```
