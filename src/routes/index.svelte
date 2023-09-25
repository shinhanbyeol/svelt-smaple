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
    return this.redirect(301, `/page/${appData.fields.pages[0].slug}`);
  }
</script>
