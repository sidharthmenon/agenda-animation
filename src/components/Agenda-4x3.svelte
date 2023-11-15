<script>
  export let content;
  export let selected;

</script>

{#if selected}
  <div class="content" id="content" bind:this={content}>
    <div class="category">{selected.category}</div>
    <div class="title">{selected.name}</div>
    {#if selected.speakers}
      <div class="speakers">
        {#each Object.entries(selected.speakers) as [category, speaker_list]}
          {#each speaker_list as {name, designation, organisation, photo, linkedin}}  
            <div class="speaker icon-{speaker_list.length}">
              
                <div class="image">
                  <img src="{photo}" alt="name" class="">
                </div>
                <div>
                  <div class="name">{name}</div>
                  <div class="designation">{designation}</div>
                  <div class="organisation">{organisation}</div>
                </div>

            </div>
          {/each}
        {/each}
      </div>
    {/if}
  </div>
{/if}

<style lang="scss">
  :global(body) {
    margin: 0;
  }

  .content{
    width: 1920px;
    height: 1280px;
    
    // width: 2000px;
    // height: 925px;

    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    // color: white;
    background-image: url("/img/breakout.png");
    background-repeat: no-repeat;
    background-size: cover;

    padding-top: 200px;
    overflow: hidden;
  }

  .category{
      font-size: 2em;
      font-family: 'Nunito', sans-serif;
      margin-bottom: 20px;
  }

  .title{
    font-size: 4rem;
    text-align: center;
    padding: 0 8rem;
    margin-bottom: 100px;
    font-family: 'Fredoka One', sans-serif;
  }

  .speakers{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 50px;
    font-family: 'Nunito', sans-serif;
    width: 90%;
  }

  .speaker{
    width: 30%;
    padding: 10px;
    // background-color: #ccc;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    gap: 10px;

    .image{
      width: 40%;
      flex-shrink: 0;
      img{
        max-width: 100%;
        border-radius: 100%;
        border: 5px solid white;
      }
    }

    .name{
      font-size: 2.5em;
      font-weight: bold;
    }

    .designation, .organisation{
      font-size: 1.5em;
    }

  }

</style>