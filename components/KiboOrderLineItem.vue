<template>
  <div data-testid="shipping-method">
    <div :key="item.id" class="productRow">
      <SfImage
        class="sf-gallery__thumb"
        :src="checkoutLineItemGetters.getProductImage(item)"
        :alt="checkoutLineItemGetters.getProductName(item)"
      />

      <div class="content">
        <div class="content__productName">
          {{ checkoutLineItemGetters.getProductName(item) }}
        </div>

        <div
          v-for="option in checkoutLineItemGetters.getProductOptions(item)"
          :key="option.attributeFQN"
          class="content__props"
        >
          <span class="title"> {{ option.name }}: </span> {{ option.value }} <br />
        </div>

        <div class="content__props">
          <span class="title">{{ $t("Price") }}: </span> ${{
            checkoutLineItemGetters.getProductPrice(item)
          }}
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { SfImage } from "@storefront-ui/vue"
import { checkoutLineItemGetters } from "@/lib/getters"

export default {
  name: "OrderLineItem",
  components: {
    SfImage,
  },
  props: {
    item: {
      type: Object,
      default: () => {},
    },
  },
  setup() {
    return {
      checkoutLineItemGetters,
    }
  },
}
</script>

<style lang="scss" scoped>
.productRow {
  display: flex;
  padding: var(--spacer-base) 0;
  border-bottom: 1px solid var(--_c-white-secondary);

  ::v-deep .sf-image--wrapper {
    --image-width: calc(var(--spacer-base) * 5.04);
    --image-height: calc(var(--spacer-base) * 5.04);

    @include for-desktop {
      --image-width: calc(var(--spacer-base) * 6.7);
      --image-height: calc(var(--spacer-base) * 6.7);
    }

    .sf-image {
      object-fit: contain;
    }
  }

  .content {
    display: flex;
    padding-left: var(--spacer-base);
    flex-direction: column;

    &__productName {
      padding-bottom: var(--spacer-2xs);
    }

    &__props {
      padding: 2px 0 2px 0;
      font-size: var(--font-size--sm);

      .title {
        font-weight: bold;
        font-size: var(--font-size--sm);
      }
    }
  }
}

.productRow:last-child {
  border: none;
}
</style>
