<template>
  <b-jumbotron v-bind:header="todo.title" lead="">

    <!-- Todo shown when we are not in editing mode. -->
    <div class="" v-show="!isEditing">

      <div class='header'>
          {{ todo.title }}
      </div>

      <div class='meta'>
          {{ todo.project }}
      </div>
      <div class= "extra content">
        <span class="right floated edit icon" v-on:click="showForm">
          <img class="img" id="editbtn" src= "https://maxcdn.icons8.com/Share/icon/Dusk_Wired/Editing//edit1600.png">
          <i class="edit icon"></i>
        </span>
        <span class="right floated trash icon" v-on:click="deleteTodo(todo)">
          <img class= "img" id="delbtn" src= "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAHgAAAB4CAMAAAAOusbgAAAAY1BMVEX///8AAADk5OTr6+ttbW1ycnLv7++tra3R0dE0NDS1tbW8vLwZGRna2tokJCQ4ODjGxsb5+flcXFyOjo6goKArKytmZmaUlJRGRkYeHh6BgYETExOampqIiIg/Pz96enpOTk7AAru4AAAEGklEQVRoge2aa5OqMAyGKWgVFaR4X9Tl///KBVJLr6x7TOrMGd9PO3XtI21I0qRJ8tFHH300ileLRcWjY4sZ69Xc0rjcK1Nax+TeGHsLec0MxVvtrQk+xuIuTS5rYj3y1QKzKhJ4Z4P37wKfIoFPNngVCby2wctI4MTitrG4yf49Rp0kotW539G4XUisR+5XRG73zNcSsPdFVG6ndD2v6+83ZAJvEc9siQjU5and5rbO9Soj5hrJh64DaahIyxC305nO0ng7wWWsJiN/TXIZ2xFxnbDkqCDhpodfwTT+c/4rlzEK7uoJLsVa82e4BFmQmD0Fxg9Wi6e4+OBimnfZUIGVy/K/UkVFBB7Tu1XjA2dLLHC11jW+SSfhfWIs8DIUhGrhf6uQwDzoG4skowQHfVQ3LSnYOQBL9Uf/dzxxnlKDA3s8+GFScJLmnsmhrEQLTkS1svQ4MxCDw/oPwWI+mUWQgcWcbadqGmTgPtEoJ56ZCCyOw9ebMJkI/DgqlMHDCBH4kUiEzyJUe1wMkXiiRkhmXH0OMFWbpHuPlz2XB2sLhJ6rC35ZcwyRSV1meu+CfoBMCU7P/RQzP9kPTh/Dr7RkMpkGzL3kADiREfxvKJ5xzlW5SCXvsiorhk8fHiUETvuzRv63Uyqv8+12e1CrtDNX7XroP7054LaqNXDC1/v1H9sx0kGPb+9J51qfjuC5ViL4xwbQVU6ktNeq3/yur7sGnr0OhnT2rBnTbrTO4mJMjQpOhy8f/NVIqDHdXeNCACeGFVvam/uACx48hvQ6ohqkAjKY7sOokcFQkoXqmCw6qDcSbEvtOS4YKiuNBlbJTwHVDbX/uGDp4n1gyEkaZfG4YL4Zl9cCg23V6l9xwQJ64CsP+KhtPz5YTjG4xaVpXBCqxjCLDIbObN3vpDD6KpIzni2QweA0724EhoXfjBMjg9PG2FjnF40DyOAMrMt1mnC00C5cIIOl8bqtI2ccG/wt57LEL5Ztae1yHDA4zdYehoBp3DBBBgOhtCcA22p1a0cGy62zrcuxLXSwDLt2L6N1bQ4b7LWuLHfXARsMmebdHCygHG/4FWwwxIaNWYIA28oNT4oNtjOeQZAS1cYYNlhA/DNPe9DkMjuV2GBpwDd9SP4Y09TRwTvXrGXjwyz0oYMhq8u5M2SdedHBMuXRzzGQ6DXEYO6GZHAq1u0ldLB0mlpNT+aeVj0FH+w4TdnNswIHPtgJgbDrB2tSfDDY8KYqpFJ4wez7LPjgFNKcUqmx154ILM7Mp2sIjFB8keCjF2znBqpxvR/vDZSv3anae8H2wzw6nt3pIrvIv1+8qOjtZV7sJoGQZbX+9ZaXfy4vXiJL2cZR46TaXSp83pQzCNzFvGzuu5cvznGPfJMKzrXvxLiv99FHH71fP130L9rBgJYGAAAAAElFTkSuQmCC">
          <i class="trash icon"></i>
        </span>
      </div>
    </div>

      <!-- <div class='' id="showform">
        <span class='' v-on:click="showForm">
            <i class='edit icon'></i>
            <img class="img" id="editbtn" src= "https://maxcdn.icons8.com/Share/icon/Dusk_Wired/Editing//edit1600.png">
        </span>

        <span class='right floated trash icon' v-on:click="deleteTodo(todo)">
          <i class='trash icon'></i>
          <img class= "img" id="delbtn" src= "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAHgAAAB4CAMAAAAOusbgAAAAY1BMVEX///8AAADk5OTr6+ttbW1ycnLv7++tra3R0dE0NDS1tbW8vLwZGRna2tokJCQ4ODjGxsb5+flcXFyOjo6goKArKytmZmaUlJRGRkYeHh6BgYETExOampqIiIg/Pz96enpOTk7AAru4AAAEGklEQVRoge2aa5OqMAyGKWgVFaR4X9Tl///KBVJLr6x7TOrMGd9PO3XtI21I0qRJ8tFHH300ileLRcWjY4sZ69Xc0rjcK1Nax+TeGHsLec0MxVvtrQk+xuIuTS5rYj3y1QKzKhJ4Z4P37wKfIoFPNngVCby2wctI4MTitrG4yf49Rp0kotW539G4XUisR+5XRG73zNcSsPdFVG6ndD2v6+83ZAJvEc9siQjU5and5rbO9Soj5hrJh64DaahIyxC305nO0ng7wWWsJiN/TXIZ2xFxnbDkqCDhpodfwTT+c/4rlzEK7uoJLsVa82e4BFmQmD0Fxg9Wi6e4+OBimnfZUIGVy/K/UkVFBB7Tu1XjA2dLLHC11jW+SSfhfWIs8DIUhGrhf6uQwDzoG4skowQHfVQ3LSnYOQBL9Uf/dzxxnlKDA3s8+GFScJLmnsmhrEQLTkS1svQ4MxCDw/oPwWI+mUWQgcWcbadqGmTgPtEoJ56ZCCyOw9ebMJkI/DgqlMHDCBH4kUiEzyJUe1wMkXiiRkhmXH0OMFWbpHuPlz2XB2sLhJ6rC35ZcwyRSV1meu+CfoBMCU7P/RQzP9kPTh/Dr7RkMpkGzL3kADiREfxvKJ5xzlW5SCXvsiorhk8fHiUETvuzRv63Uyqv8+12e1CrtDNX7XroP7054LaqNXDC1/v1H9sx0kGPb+9J51qfjuC5ViL4xwbQVU6ktNeq3/yur7sGnr0OhnT2rBnTbrTO4mJMjQpOhy8f/NVIqDHdXeNCACeGFVvam/uACx48hvQ6ohqkAjKY7sOokcFQkoXqmCw6qDcSbEvtOS4YKiuNBlbJTwHVDbX/uGDp4n1gyEkaZfG4YL4Zl9cCg23V6l9xwQJ64CsP+KhtPz5YTjG4xaVpXBCqxjCLDIbObN3vpDD6KpIzni2QweA0724EhoXfjBMjg9PG2FjnF40DyOAMrMt1mnC00C5cIIOl8bqtI2ccG/wt57LEL5Ztae1yHDA4zdYehoBp3DBBBgOhtCcA22p1a0cGy62zrcuxLXSwDLt2L6N1bQ4b7LWuLHfXARsMmebdHCygHG/4FWwwxIaNWYIA28oNT4oNtjOeQZAS1cYYNlhA/DNPe9DkMjuV2GBpwDd9SP4Y09TRwTvXrGXjwyz0oYMhq8u5M2SdedHBMuXRzzGQ6DXEYO6GZHAq1u0ldLB0mlpNT+aeVj0FH+w4TdnNswIHPtgJgbDrB2tSfDDY8KYqpFJ4wez7LPjgFNKcUqmx154ILM7Mp2sIjFB8keCjF2znBqpxvR/vDZSv3anae8H2wzw6nt3pIrvIv1+8qOjtZV7sJoGQZbX+9ZaXfy4vXiJL2cZR46TaXSp83pQzCNzFvGzuu5cvznGPfJMKzrXvxLiv99FHH71fP130L9rBgJYGAAAAAElFTkSuQmCC">
        </span>
      </div>

    </div> -->

    <!-- form is visible when we are in editing mode -->
    <div class="" v-show="isEditing">

      <div class=''>

        <div class=''>
          <label>Title</label>
          <input type='text' v-model="todo.title">
        </div>

        <div class=''>
          <label>Project</label>
          <input type='text' v-model="todo.project">
        </div>

        <div class=''>
          <button class='' v-on:click="hideForm">
            Close X
          </button>
        </div>

      </div>

    </div>

    <div class='ui bottom attached green basic button' v-show="!isEditing &&todo.done" disabled>
        Completed
    </div>

    <div class='ui bottom attached red basic button' v-on:click="completeTodo(todo)" v-show="!isEditing && !todo.done">
        Pending
    </div>

  </b-jumbotron>
</template>

<script>
export default {
  props: ['todo'],
  data () {
    return {
      isEditing: false
    }
  },
  methods: {
    completeTodo (todo) {
      this.$emit('complete-todo', todo)
    },
    deleteTodo (todo) {
      this.$emit('delete-todo', todo)
    },
    showForm () {
      this.isEditing = true
    },
    hideForm () {
      this.isEditing = false
    }
  }
}
</script>

<style>
.img {
  width  : 25px;
  height : 25px;
  float: right;
}
</style>
