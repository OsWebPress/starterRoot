<script setup>
import { useSlots, onMounted } from 'vue'

const slots = useSlots()
const children = slots.default()[0].children;
document.title = children[0].props.innerHTML;

const props = defineProps({
  title: {
    type: String,
    required: true
  }
})
  
</script>
