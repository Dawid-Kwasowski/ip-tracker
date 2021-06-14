<template>
  <section class="mt-5 mb-2">
    <div class="card">
      <div class="card-body">
        <slot name="card-title" class="card-title">
          <h2>Nothing Special</h2>
        </slot>
        <hr />
        <slot name="card-text" class="card-text">
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum necessitatibus
            cupiditate iusto quo commodi quos ea saepe, nihil eius perferendis nemo
            corrupti nostrum placeat aut facere, culpa odit nisi! Alias!
          </p>
        </slot>
      </div>
    </div>
  </section>
</template>
