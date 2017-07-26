# WordPress Tricks

Use the WordPress `locate_template()` function within PHP’s `include()`, instead of `get_template_part()`.

	<?php
	$var = 'Hello World!';
	include(locate_template('file/path/filename.php'));
	?>

## Change name of "Post"

Example of `functions.php` addition if you want to change "Posts" to "News"

	function newproject_change_post_label() {
	    global $menu;
	    global $submenu;
	    $menu[5][0] = 'News';
	    $submenu['edit.php'][5][0] = 'News';
	    $submenu['edit.php'][10][0] = 'Add News';
	    $submenu['edit.php'][16][0] = 'News Tags';
	}
	function newproject_change_post_object() {
	    global $wp_post_types;
	    $labels = &$wp_post_types['post']->labels;
	    $labels->name = 'News';
	    $labels->singular_name = 'News';
	    $labels->add_new = 'Add News';
	    $labels->add_new_item = 'Add News';
	    $labels->edit_item = 'Edit News';
	    $labels->new_item = 'News';
	    $labels->view_item = 'View News';
	    $labels->search_items = 'Search News';
	    $labels->not_found = 'No News found';
	    $labels->not_found_in_trash = 'No News found in Trash';
	    $labels->all_items = 'All News';
	    $labels->menu_name = 'News';
	    $labels->name_admin_bar = 'News';
	} add_action( 'admin_menu', 'newproject_change_post_label' );
	add_action( 'init', 'newproject_change_post_object' );

## Add Custom Post Type

	function newproject_work_post_type () {
		$labels = array (
			'name' => 'Work',
			'singular_name' => 'Work Item',
			'add_new' => 'Add Work Item',
			'all_items' => 'All Work',
			'add_new_item' => 'Add Work Item',
			'edit_item' => 'Edit Work Item',
			'new_item' => 'New Work Item',
			'view_item' => 'View Work Item',
			'search_item' => 'Search Work',
			'not_found' => 'No Work Items Found',
			'not_found_in_trash' => 'No Work Found In Trash',
			'parent_item_colon' => 'Parent Work Item'
		);
		$work = array(
			'labels' => $labels,
			'public' => true,
			'has_archive' => true,
			'publicly_queryable' => true,
			'query_var' => true,
			'rewrite' => true,
			'capability_type' => 'post',
			'hierarchical' => false,
			'supports' => array(
				'title',
				'editor',
				'thumbnail',
				'revisions',
			),
			'taxonomies' => array('category', 'post_tag'),
			'menu_position' => 5,
			'exclude_from_search' => false
		);
		register_post_type('work',$work);
	} add_action('after_setup_theme', 'newproject_work_post_type');

## ACF Relationship Field Nested Witin Repeater Field + Reverse Query

General navigation of a complex post/post relationship.

### ACF Relationship Field Nested Witin Repeater Field



### Reverse Query

Add this function to `functions.php` and change `parent` and `child` to corresponding field name.

	function my_posts_where( $where ) {
	    $where = str_replace("meta_key = 'parent_%_child'", "meta_key LIKE 'parent_%_child'", $where);
	    return $where;
	} add_filter('posts_where', 'my_posts_where');

Code for the page you want to display the Reverse Query on. Change `posts` in `'post_type' =>` if you are trying to display a custom post type and then change `parent` and `child` to corresponding field name.

	// args
	$args = array(
	    'post_type' => 'posts',
	    'meta_query' => array(
	        array(
	            'key' => 'parent_%_child',
	            'value' => '"' . get_the_ID() . '"',
	            'compare' => 'LIKE'
	        )
	    )
	);
	 
	// get results
	$the_query = new WP_Query( $args );
	 
	// The Loop
	?>
	<?php if( $the_query->have_posts() ): ?>
	    <ul>
	    <?php while ( $the_query->have_posts() ) : $the_query->the_post(); ?>
	        <li>
	            <a href="<?php the_permalink(); ?>"><?php the_title(); ?></a>
	        </li>
	    <?php endwhile; ?>
	    </ul>
	<?php endif; wp_reset_query(); ?>