<!--
/**
 * Copyright (c) 2020, 2022, Oracle and/or its affiliates.
 * Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
 */
-->

<script>
  export let headerRenditionURLs = "";
  export let pages;

  import { stores } from '@sapper/app';
  const { page } = stores();
  let currentPageSlug;
  $ : {
    let params = $page.path.split('/');
    currentPageSlug = params.pop();
  }

  /*
   * Show/hide the drop down menu in narrow screens when the
   * button is clicked and update the button styling.
   */
  function onDropDownMenuButtonClicked() {
    if (document) {
      const dropDownMenu = document.getElementById("nav-menu-items");
      const menuButton = document.getElementById("nav-menu-button");
      console.log(dropDownMenu);
      if (dropDownMenu.className === "") {
        dropDownMenu.className = "displayed";
        menuButton.className = "active";
      } else {
        dropDownMenu.className = "";
        menuButton.className = "";
      }
    }
  }

</script>

<header id="header">
  <a href="page/{pages[0].slug}" style="text-decoration:none">
    <picture>
      <source type="image/webp" srcset={headerRenditionURLs.srcset} />
      <img id="header-image" src={headerRenditionURLs.native} alt="Company Logo"
        width={headerRenditionURLs.width} height={headerRenditionURLs.height}/>
    </picture>
  </a>

  <nav>
    <button
      id="nav-menu-button"
      on:click={onDropDownMenuButtonClicked}
      type="button">
      ☰
    </button>

    <ul id="nav-menu-items">
      {#each pages as page}
      <li>
        <a
          href="page/{page.slug}"
          sapper:prefetch
          id="{page.slug}"
          class={currentPageSlug === page.slug ? 'active' : ''}
          style="text-decoration:none">
          {page.name}
        </a>
      </li>
      {/each}
    </ul>
  </nav>
</header>
