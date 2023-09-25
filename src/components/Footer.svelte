<!--
/**
 * Copyright (c) 2020, 2022, Oracle and/or its affiliates.
 * Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
 */
-->

<script>
  export let footerRenditionURLs;
</script>

<footer id="footer">
  <!-- {/* Logo */} -->
  <picture>
    <source type="image/webp" srcset={footerRenditionURLs.srcset} sizes="300px" />
    <img id="footer-image" src={footerRenditionURLs.native} alt="Footer Logo"
      width="{footerRenditionURLs.width}" height="{footerRenditionURLs.height}"/>
  </picture>
  <div class="social-media-menu">
    <a href="https://www.facebook.com/Oracle/">
      <img src="images/facebook.png" alt="Facebook" loading="lazy" />
    </a>
    <a href="https://www.linkedin.com/company/oracle/">
      <img src="images/linkedin.png" alt="Linked In" loading="lazy" />
    </a>
    <a href="https://twitter.com/Oracle">
      <img src="images/twitter.png" alt="Twitter" loading="lazy" />
    </a>
    <a href="https://www.youtube.com/oracle/">
      <img src="images/youtube.png" alt="You Tube" loading="lazy" />
    </a>
  </div>
</footer>
