<script lang="ts">
import { defineComponent, h, isVue2, onBeforeUnmount, onMounted } from "vue-demi";
import { useTonConnectUI } from "../hooks/useTonConnectUI";

export default defineComponent({
  name: "TonConnectButton",
  props: {
    buttonRootId: {
      type: String,
      default: "ton-connect-button",
    },
  },
  setup(
    props: { buttonRootId?: string },
    { slots }
  ) {
    const {setOptions} = useTonConnectUI();
    const attrs = isVue2
        ? { attrs: { id: props.buttonRootId || "" } }
        : {};
    onMounted(() => {
      setOptions({ buttonRootId: props.buttonRootId });
    });

    onBeforeUnmount(() => {
      setOptions({ buttonRootId: null });
    });

    return () => {
      return h(
        "div",
        {
          id: props.buttonRootId || "",
          style: { width: "fit-content" },
          ...attrs
        } as any,
        (slots as any)?.default?.()
      );
    };
  },
});
</script>
