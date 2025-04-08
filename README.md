# elementor-avif-patch

Description: Automatically patches Elementor's frontend.js to support .avif in lightbox.

**🧩 Here's how to do it with WPCode:**
Go to WPCode » Code Snippets → Add New

Choose "PHP Snippet"

Name it something like: Elementor AVIF Patch

Paste this code:

````
add_action('init', function () {
    $plugin_path = WP_PLUGIN_DIR . '/elementor/assets/js/frontend.js';
    $plugin_min_path = WP_PLUGIN_DIR . '/elementor/assets/js/frontend.min.js';

    if (file_exists($plugin_path)) {
        $contents = file_get_contents($plugin_path);
        if (strpos($contents, '|avif') === false) {
            $patched = preg_replace('/svg\\|webp/', 'svg|webp|avif', $contents);
            file_put_contents($plugin_path, $patched);
        }
    }

    if (file_exists($plugin_min_path)) {
        $min_contents = file_get_contents($plugin_min_path);
        if (strpos($min_contents, '|avif') === false) {
            $patched_min = preg_replace('/svg\\|webp/', 'svg|webp|avif', $min_contents);
            file_put_contents($plugin_min_path, $patched_min);
        }
    }
});
````


✅ What It Does:
Auto-patches frontend.js and frontend.min.js in Elementor on every load

Adds .avif support to the lightbox

Shows an admin notice after Elementor updates, when it reapplies the patch

If you are not comfortable with the PHP snippets / custom function php just use the plugin (upload the zip file)
