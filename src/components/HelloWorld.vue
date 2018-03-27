<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <p>
            For guide and recipes on how to configure / customize this project,<br>
            check out the
            <a href="https://github.com/vuejs/vue-cli/tree/dev/docs" target="_blank">vue-cli documentation</a>.
        </p>
        <h3>Installed CLI Plugins</h3>
        <ul>
            <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank">babel</a>
            </li>
            <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank">eslint</a>
            </li>
        </ul>
        <h3>Essential Links</h3>
        <ul>
            <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
            <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
            <li><a href="https://chat.vuejs.org" target="_blank">Community Chat</a></li>
            <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
        </ul>
        <h3>Ecosystem</h3>
        <ul>
            <li><a href="https://router.vuejs.org/en/essentials/getting-started.html" target="_blank">vue-router</a>
            </li>
            <li><a href="https://vuex.vuejs.org/en/intro.html" target="_blank">vuex</a></li>
            <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank">vue-devtools</a></li>
            <li><a href="https://vue-loader.vuejs.org/en" target="_blank">vue-loader</a></li>
            <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
        </ul>
        <div class="apollo">
            <!--<div v-for="user in users">-->
            <!--<h2>{{ user.name }}</h2>-->
            <!--</div>-->
            <h1> {{ msg }}</h1>
            <h1> {{ users }}</h1>
            <h1> {{ hello }}</h1>
            <div v-if="$apollo.loading">Loading...</div>
        </div>
        <ApolloQuery
                :query="require('../graphql/Hello.gql')"
        >
            <template slot-scope="{ result: { loading, error, data } }">
                <!-- Loading -->
                <div v-if="loading" class="loading apollo">Loading...</div>

                <!-- Error -->
                <div v-else-if="error" class="error apollo">An error occured</div>

                <!-- Result -->
                <div
                        v-else-if="data"
                        v-for="user of data.users"
                        :key="user.name"
                        class="message"
                >
                    {{ user.name }}
                    {{ user.balance }}
                </div>

                <!-- No result -->
                <div v-else class="no-result apollo">No result :(</div>
            </template>
        </ApolloQuery>
    </div>

</template>

<script>
    import gql from 'graphql-tag'

    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        apollo: {
            // Simple query that will update the 'hello' vue property
            hello: gql`{ hello }`,
        },
        data() {
            return {
                hello: '',
                users: []
            }
        },
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
