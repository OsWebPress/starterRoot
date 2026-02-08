<script setup>
const props = defineProps({
  title: {
    type: String,
    required: true
  }
})
document.title = props.title;
</script>