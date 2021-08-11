<!DOCTYPE html>
<html <?php language_attributes(); ?>>
    <head>        
        <meta charset="<?php bloginfo('charset'); ?>" />        
        <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />        		
        <?php wp_head(); ?>        
    </head>    
    <body <?php body_class(); ?>>
        <?php wp_body_open(); ?>

        <div class="doc-loader">
            <?php if ((get_option('cocobasic_preloader') !== '') && (get_option('cocobasic_preloader') !== false)): ?>                
                <img src="<?php echo esc_url(get_option('cocobasic_preloader', get_template_directory_uri() . '/images/preloader.gif')); ?>" alt="<?php echo esc_attr(get_bloginfo('name')); ?>" />
            <?php endif; ?>
        </div>  

        <header>             

            <div class="header-right-part-holder">
                <div class="header-right-part">
                    <div class="header-logo">
                        <?php if (get_option('cocobasic_header_logo') !== ''): ?>
                            <a href="<?php echo esc_url(home_url('/')); ?>">
                                <img src="<?php echo esc_url(get_option('cocobasic_header_logo', get_template_directory_uri() . '/images/logo.png')); ?>" alt="<?php echo esc_attr(get_bloginfo('name')); ?>" />
                            </a>
                        <?php endif; ?>                   
                    </div>

                    <div class="toggle-holder">
                        <div id="toggle">                    
                            <div></div>                    
                            <div></div>                    
                            <div></div>                    
                        </div>
                    </div>
                </div>
            </div>

            <div class="header-full-menu">
                <div class="menu-wrapper center-relative relative">             
                    <?php if ((get_theme_mod('cocobasic_custom_menu_text') !== '') && (get_theme_mod('cocobasic_custom_menu_text') !== false)): ?>  
                        <div class="custom-menu-title">                        
                            <?php echo esc_html(get_theme_mod('cocobasic_custom_menu_text')); ?>
                        </div>
                    <?php endif; ?>
                    <div class="menu-holder">                        
                        <?php
                        if (has_nav_menu("custom_menu")) {
                            wp_nav_menu(
                                    array(
                                        "container" => "nav",
                                        "container_id" => "header-main-menu",
                                        "fallback_cb" => false,
                                        "menu_class" => "main-menu sm sm-clean",
                                        "theme_location" => "custom_menu",
                                        "items_wrap" => '<ul id="%1$s" class="%2$s">%3$s</ul>',
                                        "walker" => new Cocobasic_Header_Menu()
                                    )
                            );
                        } else {
                            echo '<nav id="header-main-menu" class="default-menu"><ul>';
                            wp_list_pages(array("depth" => "3", 'title_li' => ''));
                            echo '</ul>';
                            echo '</nav>';
                        }
                        ?>                       
                    </div>                    
                    <?php if (get_theme_mod('cocobasic_select_menu_text') != '') : ?>
                        <div class="menu-text-holder">
                            <?php cocobasic_show_elementor_library_content(get_theme_mod('cocobasic_select_menu_text')); ?>
                        </div>
                    <?php endif;
                    ?>     

                    <div class="clear"></div>   
                </div>
            </div>
        </header>                      
