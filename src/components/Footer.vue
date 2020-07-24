

<template>
    <div class="footer">
        <p>Made with <span>♥</span> using <b>VueJS</b> and <b>MongoDB</b><br/>Cedric-F</p>
        <div class="social-links">
            <a href="https://linkedin.com/in/Cedric-F" target="_blank" title="LinkedIn"><i class="fab fa-linkedin"/></a>
            <a href="https://github.com/Cedric-F" target="_blank" title="GitHub"><i class="fab fa-github-square"/></a>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Footer"
    }
</script>

<style scoped>
    .footer {
        display: flex;
        justify-content: center;
        align-items: center;
        background: #2c3e50;
        position: relative;
    }

    .social-links {
        position: absolute;
        bottom: 10px;
        right: 10px;
        width: 50px;
        display: flex;
        justify-content: space-between;
        justify-items: center;
    }

    .fab {
        font-size: 1.5rem;
        color: #00ffdb;
    }

    span {
        color: red;
        font-size: 1.5rem;
        text-shadow: white 1px 1px 1px;
    }
</style>