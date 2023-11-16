<script>
  export let content;
  export let selected;

  $:selected_count = selected && selected.speakers ? Object.values(selected.speakers).flat(1).length : 0 ;

</script>

{#if selected}
  <div class="content" id="content" bind:this={content}>
    <div class="category">{selected.category ?? ""}</div>
    <div class="title">{selected.name}</div>
    {#if selected.speakers}
      <div class="speakers {selected_count > 6 ? "extended" : ""}">
        {#each Object.entries(selected.speakers) as [category, speaker_list]}
          {#each speaker_list as {name, designation, organisation, photo, linkedin}}  
            <div class="speaker  icon-{speaker_list.length} {selected_count == 1 ? "single" : ""}">
              
                <div class="image">
                  <img src="{photo}" alt="name" class="">
                </div>
                <div class="details">
                  <div class="name">{name}</div>
                  <div class="designation">{designation}</div>
                  <div class="organisation">{organisation ?? ''}</div>
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
    // width: 2000px;
    // height: 1300px;
    
    width: 3840px;
    height: 2160px;

    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    // color: white;
    background-image: url("/img/breakout.jpg");
    background-repeat: no-repeat;
    background-size: cover;

    // padding-top: 200px;
    overflow: hidden;
  }

  .category{
      font-size: 4em;
      font-family: 'Poppins', sans-serif;
      margin-bottom: 20px;
      width: 100%;
      text-align: center;
  }

  .title{
    font-size: 6rem;
    text-align: center;
    padding: 0 8rem;
    margin-bottom: 100px;
    font-family: 'Barlow', sans-serif;
    font-weight: 900;
    width: 75%;
  }

  .speakers{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 50px;
    font-family: 'Poppins', sans-serif;
    width: 80%;

    &.extended{
      width: 100%;

      .speaker{
        width : 20%;
      }

    }
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

    &.single{
      width: 50%;

      .image{
        width: 50%;

        img{
          height: 500px;
        }
      }

      .name{
        font-size: 4em;
      }

      .designation, .organisation{
        font-size: 3em;
      }
    }

    &.horizontal{
      flex-direction: row;
      text-align: left;

      .details{
        text-align: left;
      }
    }

    .image{
      width: 30%;
      flex-shrink: 0;
      img{
        max-width: 100%;
        border-radius: 100%;
        border: 8px solid #ef4444;
        border-top: 0;
        border-left: 0;
      }
    }

    .name{
      font-size: 3em;
      font-weight: bold;
    }

    .designation, .organisation{
      font-size: 2em;
      margin: 0 auto;
      padding-bottom: 1px;
    }

    .details{
      text-align: center;
      width: 100%;
    }

  }

</style>