<script setup>
const router = useRouter(); //to get access to the Vue Router instance. The router allows for programmatic navigation between different pages of your app.
const token = useCookie("token"); // to retrieve a cookie named "token". It’s often used to handle authentication tokens stored in the user's browser.
import { useAuthStore } from '~/store/useAuthStore'; //for managing authentication-related state.

const { sessionWatcher } = useAuthStore(); //probably checks whether the user's session is still valid 
const { authenticated } = storeToRefs(useAuthStore()); //to convert store properties into reactive references.


onMounted(() => {
  sessionWatcher(); //to check the session as soon as the component is mounted.
  setInterval(() => { //ensures that the session status is continuously checked and updated.
    sessionWatcher();
  }, 10000);
});
</script>
<template> 
  <div>
    <NuxtLayout> 
      <NuxtLoadingIndicator />
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>


