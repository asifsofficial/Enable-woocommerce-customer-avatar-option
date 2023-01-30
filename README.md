# Enable woocommerce customer avatar option
## Location
```
functions.php
```
```
// Add custom avatar upload field to WooCommerce account page
function add_custom_avatar_upload_field() {
    $user_id = get_current_user_id();
    $avatar = get_user_meta($user_id, 'avatar', true);
    ?>
    <h3>Profile Picture</h3>
    <table class="form-table">
        <tr>
            <th><label for="avatar">Upload Profile Picture</label></th>
            <td>
                <?php if ($avatar) { ?>
                    <img src="<?php echo esc_url($avatar); ?>" width="100" height="100" />
                    <br /><br />
                <?php } ?>
                <input type="file" name="avatar" id="avatar" />
                <br />
                <span class="description">Upload your profile picture</span>
            </td>
        </tr>
    </table>
    <?php
}
add_action('woocommerce_edit_account_form', 'add_custom_avatar_upload_field');

// Save custom avatar uploaded in WooCommerce account page
function save_custom_avatar_upload($user_id) {
    if (!empty($_FILES['avatar']['name'])) {
        $avatar = wp_handle_upload($_FILES['avatar'], array('test_form' => false));
        update_user_meta($user_id, 'avatar', $avatar['url']);
    }
}
add_action('woocommerce_save_account_details', 'save_custom_avatar_upload');
```
