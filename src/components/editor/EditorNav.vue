<template>
    <section class="editor-nav flex flex-nowrap text-center">

        <div class="flex-grow" title="Add New Section" @click="setEditorScreen('editor-add-section')">
            <font-awesome-icon :icon="['fas', 'plus']" />
            <div class="editor-nav-item-label"> Section </div>
        </div>
        <div class="flex-grow" title="Add New Elements" @click="setEditorScreen('editor-add-element')">
            <font-awesome-icon :icon="['fas', 'th']" />
            <div class="editor-nav-item-label"> Elements </div>
        </div>
        <div class="flex-grow" title="Elements Tree" @click="setEditorScreen('editor-elements-tree')">
            <font-awesome-icon :icon="['fas', 'cog']" />
            <div class="editor-nav-item-label"> Tree </div>
        </div>

    </section>
</template>

<script>
export default {
    name: 'editor-nav',
    methods: {
        setEditorScreen(screen) {
           this.$store.commit({ type: 'setEditorScreen', screen });
        }
    }
};
</script>

<style scoped lang="scss">
.editor-nav {
    padding: 0;
    margin-bottom: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    background-color: #fff;
    cursor: pointer;

    > div {
        padding: 15px 0 10px;
        font-size: 20px;
        color: #333;
        transition: 1s;

        &:hover {
            background-color: #eee;
            transition: .25s;
        }

        .editor-nav-item-label {
            padding-top: 10px;
            font-size: 13px;
        }
    }
}
</style>
