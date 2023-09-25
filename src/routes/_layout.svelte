<!--
/**
 * Copyright (c) 2020, 2022, Oracle and/or its affiliates.
 * Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
 */
-->

<script context="module">
  import { fetchOceMinimalMain } from "../scripts/services.js";

  export async function preload() {
    const appData = await fetchOceMinimalMain();
    return {
      appData,
    };
  }
</script>

<script>
  export let appData;

  import Header from "../components/Header.svelte";
  import Footer from "../components/Footer.svelte";

  const { headerRenditionURLs, footerRenditionURLs, fields } = appData;
  const pages = fields.pages;
</script>

<Header {headerRenditionURLs} {pages} />
<main>
  <slot />
</main>
<Footer {footerRenditionURLs} />
