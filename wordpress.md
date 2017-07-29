# WordPress Tricks

Use the WordPress `locate_template()` function within PHP’s `include()`, instead of `get_template_part()`.

	<?php
	$var = 'Hello World!';
	include(locate_template('file/path/filename.php'));
	?>

## Human Time Conversion

This examplue uses a hypothetical ACF called "date" (called with `get_field('date')`)

	This post was made <?php echo human_time_diff( strtotime(get_field('date')), current_time( 'timestamp' ) ); ?> ago

## Link to a page by name

Three ways to link to a wordpress page based on its name

	<a href="<?php echo get_permalink( get_page_by_path( 'map' ) ) ?>">Link</a>
	<a href="<?php echo get_permalink( get_page_by_title( 'Map' ) ) ?>">Link</a>
	<a href="<?php echo home_url( '/map/' ) ?>">Link</a>

## Check for empty Content

If you want to only display the post if it has content, first add this function to `functions.php`

	function empty_content($str) {
	    return trim(str_replace('&nbsp;','',strip_tags($str))) == '';
	}

Then wrap the content in the loop in

	if (!empty_content($post->post_content)) {
		the_content();
	} else {
		You didn't put any content in the post
	}

## Sort Search Results by Custom Post Type

This example includes a structure that dynamically pulls content from templates. The templates that will be dynamically pulled will correspond with the `$query_type` and the `$types`. For the below code, 4 temples would need to be created in the `parts/content` folder:

-`search-post.php`
-`search-custom_type_1.php`
-`search-custom_type_2.php`
-`search-custom_type_4.php`

And cycle through the loop with:

	<?php
	if( have_posts() ){
	    $types = array('post', 'custom_type_1', 'custom_type_2', 'custom_type_4');
	    $query_type = 'search';
	    foreach( $types as $type ){
	        while( have_posts() ){
	            the_post();
	            if( $type == get_post_type() ){
	                get_template_part('parts/content/' . $query_type, $type);
	            }
	        }
	        rewind_posts();
	    }
	}
	?>

## ACF Google Map API

To use the Google Maps ACF plugin, first register a Google Maps API key
[https://developers.google.com/maps/documentation/javascript/get-api-key](https://developers.google.com/maps/documentation/javascript/get-api-key)

Add jquery, API script with API Key, and this minified script to `header`

	<script src="https://code.jquery.com/jquery-3.1.1.min.js" integrity="sha256-hVVnYaiADRTO2PzUGmuLJr8BLUSjGIZsDYGmIJLv2b8=" crossorigin="anonymous"></script>
	<script src="https://maps.googleapis.com/maps/api/js?key=xxxxxxxxxxxxxxxxxxx_xxxxxxxxxxx"></script>
	<script type="text/javascript">
		!function(n){function e(e){var t=e.find(".marker"),r={zoom:16,center:new google.maps.LatLng(0,0),mapTypeId:google.maps.MapTypeId.ROADMAP},g=new google.maps.Map(e[0],r);return g.markers=[],t.each(function(){a(n(this),g)}),o(g),g}function a(n,e){var a=new google.maps.LatLng(n.attr("data-lat"),n.attr("data-lng")),o=new google.maps.Marker({position:a,map:e});if(e.markers.push(o),n.html()){var t=new google.maps.InfoWindow({content:n.html()});google.maps.event.addListener(o,"click",function(){t.open(e,o)})}}function o(e){var a=new google.maps.LatLngBounds;n.each(e.markers,function(n,e){var o=new google.maps.LatLng(e.position.lat(),e.position.lng());a.extend(o)}),1==e.markers.length?(e.setCenter(a.getCenter()),e.setZoom(16)):e.fitBounds(a)}var t=null;n(document).ready(function(){n(".acf-map").each(function(){t=e(n(this))})})}(jQuery);
	</script>

Paste the Key into the following code and put it in `functions.php`

	function my_acf_google_map_api( $api ){
		
		$api['key'] = 'xxxxxxxxxxxxxxxxxxx_xxxxxxxxxxx';
		return $api;
		
	} add_filter('acf/fields/google_map/api', 'my_acf_google_map_api');

Executing the map on the page. The code will need to be within the Loop.

	<div class="about-offices">

		<div class="about-office">

			<?php if (get_field('office__address')) { ?>

				<div class="about-address">

					<?php the_field('office__address'); ?>

				</div>

			<?php } ?>

			<?php if (get_field('office__map')) { ?>

				<?php $location = get_field('office__map'); ?>

				<?php if( !empty($location) ): ?>
				<div class="acf-map">
					<div class="marker" data-lat="<?php echo $location['lat']; ?>" data-lng="<?php echo $location['lng']; ?>"></div>
				</div>
				<?php endif; ?>

			<?php } ?>

		</div>

	</div>

Last, style the .acf-map class and add this conflict fix to the css

	.acf-map {
	    width: 100%;
	    height: 400px;
	}

	/* fixes potential theme css conflict */
	.acf-map img {
	    max-width: inherit !important;
	}

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