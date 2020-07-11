<template>
        <div class="box has-text-centered mt-3"  > 
            <template v-for="turn  in turns">
                <div class="notification is-light" :key="turn.index" :class="{'is-primary': turn.isPlayer, 'is-danger': !turn.isPlayer}"> 
                    <strong>{{turn.text}}</strong>
                </div>
            </template>

        </div>
</template>
<script>
export default {
    name:"Messages",
    props:{
      turns:Array
    }
};
</script>
