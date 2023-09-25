<!--
/**
 * Copyright (c) 2020, 2022, Oracle and/or its affiliates.
 * Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
 */
-->

<script context="module">
  import { fetchPage, getRenditionURLs } from "../../scripts/services.js";

  export async function preload(page) {
    // find the slug param from the page. If its null, default to home
    let slug = page.params.slug;
    if (slug == null) {
      slug = 'home';
    }
    // fetch the page corresponding to the slug
    const pageData = await fetchPage(slug);
    const { sections } = pageData.fields;

    // for each section in the page, if a image is present, get the corresponding rendition urls
    // and insert it back into the section
    const promises = [];
    sections.forEach((section) => {
      // add a promise to the total list of promises to get any section rendition urls
      if (section.fields.image) {
        promises.push(
          getRenditionURLs(section.fields.image.id)
            .then((renditionURLs) => {
              // eslint-disable-next-line no-param-reassign
              section.renditionURLs = renditionURLs;
            }),
        );
      }
    });

    // execute all the promises and return all the data
    await Promise.all(promises);
    return {
      pageData,
    };

  }
</script>

<script>
  export let pageData;
  import Section from "../../components/Section.svelte";
</script>

<svelte:head>
  <title>{pageData.name}</title>
</svelte:head>

<div key={pageData.id}>
  {#if pageData.fields.sections}
    <div id="sections">
      {#each pageData.fields.sections as section}
        <Section {section}/>
      {/each}
    </div>
  {/if}
</div>