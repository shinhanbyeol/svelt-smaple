<!--
/**
 * Copyright (c) 2020, 2022, Oracle and/or its affiliates.
 * Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
 */
-->

<script>
  export let section;
  import filterXSS from "xss";
  const options = {
    stripIgnoreTag: true, // filter out all HTML not in the whitelist
    stripIgnoreTagBody: ['script'], // the script tag is a special case, we need
    // to filter out its content
  };

  const cleantext = filterXSS(section.fields.body, options);
</script>

<section class={`content ${section.fields.type}`} key={section.id}>
  <div>
    {#if section.renditionURLs}
      <picture>
        <source type="image/webp" srcSet={section.renditionURLs.srcset} />
        <source srcSet={section.renditionURLs.jpgSrcset} />
        <img
          id="header-image"
          src={section.renditionURLs.large}
          alt="Company Logo"
          width={section.renditionURLs.width}
          height={section.renditionURLs.height}
        />
      </picture>
    {/if}
    <div>
      <h1>{section.fields.heading}</h1>
      <div class="text">
        {@html cleantext}
      </div>
      {#if section.fields.actions}
        <div>
          {#each section.fields.actions as action}
            <a class="button" href={action.link}>
              {action.name}
            </a>
          {/each}
        </div>
      {/if}
    </div>
  </div>
</section>
