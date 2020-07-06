<template>
<nav>
    <div class="menu-logo">Music App</div>
    <div class="menu-item"><a href="#">Home</a></div>
    <div class="menu-item"><a href="#">About us</a></div>
    <Dropdown title="Songs" :items="songs" />
    <div class="menu-item"><a href="#">Artists</a></div>
</nav>
</template>

<script>
import Dropdown from './Dropdown';
export default {
    name: 'navbar',
    components: {
        Dropdown
    },
    data () {
        return {
            songs: [
                {
                    title: 'Rock',
                    link: '#'
                },
                {
                    title: 'Pop',
                    link: '#'
                },
                {
                    title: 'Classic',
                    link: '#'
                },
            ]
        }
    }
}
</script>

<style>
nav {
    display: flex;
    align-items: center;
    justify-content: center;
}
nav .menu-item {
    color: #ffffff;
    padding: 7px 30px;
    position: relative;
    text-align: center;
    border-bottom: 3px solid transparent;
    display: flex;
    transition: 0.4s;
    font-size: 20px;
}
nav .menu-logo {
    font-size: 20px;
    font-weight: 900;
    padding-right: 20px;
}
nav .menu-item.active,
nav .menu-item:hover {
    border-radius: 10px;
    border-bottom-color: #471e4f;
    font-weight: 500;
}
nav .menu-item a {
    color:inherit;
    text-decoration: none;
}
</style>