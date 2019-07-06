```php
function wp_all_export_after_export( $export_id, $exportObj ) {
    if ( $exportObj->exported == 0 ) {
        $file = $exportObj->options["filepath"];
        unlink( $file );
        unlink( str_replace( basename( $file ), 'current-' . basename( $file ), $file ) );
    }	
}
add_action( 'pmxe_after_export', 'wp_all_export_after_export', 10, 2 );
```