<template>
    <div class="animate__animated animate__fadeIn">
        <transition name="fade">
            <ul id="mainMenu">
                <li class="animate__animated animate__headShake">
                    <router-link :to="{name: 'campus.home'}">Início</router-link>
                </li>
                <li class="animate__animated animate__headShake">
                    <router-link :to="{name: 'campus.my.supports'}">Minhas Dúvidas</router-link>
                </li>
                <li class="animate__animated animate__headShake">
                    <a href="#" @click.prevent="logout">
                        <span v-if="loadingStore">Saindo...</span>
                        <span v-else>Sair</span>
                    </a>
                </li>
            </ul>
        </transition>
    </div>
</template>

<script>
import { computed } from 'vue'
import { useStore } from 'vuex'

import router from "@/router"
import { notify } from '@kyvg/vue3-notification'

export default {
    name: 'MenuHeader',
    setup() {
        const store = useStore()

        const logout = () => {
            store.dispatch('logout')
                    .then(() => {
                        notify({
                            title: 'Sucesso',
                            text: 'Usuário deslogado com sucesso!',
                            type: 'success'
                        })
                        router.push({name: 'auth'})
                    })
        }
        const loadingStore = computed(() => store.state.loading)

        return {
            logout,
            loadingStore,
        }
    }
}
</script>