# Append ACF Repeater Data

It's not possible to append a row to an ACF repeater field without a custom code workaround that utilizes our API: http://www.wpallimport.com/documentation/developers/action-reference/.

The following is an *example* to show you how this can be done. You will almost certainly need to adjust the code snippet to make it work with your data/site.

1) Create a new "Manual Record Matching" import that updates the post(s): http://www.wpallimport.com/documentation/recurring/manual-record-matching/

2) Store the ACF data in your own dummy custom field: http://d.pr/i/3Si4ad.

3) Add some code in the Function Editor that grabs that data and appends it to the ACF field. 

Example code:

```php
add_action( 'pmxi_saved_post', 'soflyy_add_data', 10, 3 );

function soflyy_add_data( $id, $xml, $update ) {
	$selector = 'basic_repeater'; // The Parent field name
	$subfield1 = 'repeater_text'; // The repeating field you want to add data to
	
	if ( $value = get_post_meta( $id, 'my_repeater_data', true ) ) {
		$row = array( $subfield1 => $value );
		add_row( $selector, $row, $id );
	}
	delete_post_meta( $id, 'my_repeater_data' );
}
```

4) On step 4 of the import, choose to only update the custom field that you're importing: http://d.pr/i/WfZKAT.