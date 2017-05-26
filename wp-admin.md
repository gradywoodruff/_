# WordPress Admin Styling

Add this code to the `functions.php` file

	function admin_style() {
	wp_enqueue_style('admin-styles', get_template_directory_uri().'/assets/styles/admin.css');
	} add_action('admin_enqueue_scripts', 'admin_style');