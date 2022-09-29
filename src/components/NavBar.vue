<template>
    <nav class="navbar navbar-dark bg-success navbar-expand-sm">
        <div class="container d-flex justify">

            <div>
                <router-link to="/" class="navbar-brand"><i class="fa fa-mobile"></i> Contact Organizer</router-link>
            </div>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item">
                        <a class="nav-link " aria-current="page" href="/">Home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="/contacts">Contact List</a>
                    </li>

                </ul>
            </div>
        </div>

    </nav>

</template>
  
<script>
export default {
    name: "NavBar"
}
</script>
  
<style scoped>

</style>
  