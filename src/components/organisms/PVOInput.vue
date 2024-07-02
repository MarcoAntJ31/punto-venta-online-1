<template>
    <div class="w-100 h-auto">
        <label class="label" v-if="label">{{ labelMessage }}</label>
        <v-text-field
            v-if="type !== 'textarea'"
            @update:model-value="updateModel($event)"
            :model-value="modelValue"
            :type="type"
            :class="aInputCustomClass"
            :clearable="clearable"
            :placeholder="placeholder"
            :readonly="readonly"
            :disabled="disabled"
            :prepend-icon="prependIcon"
            :prepend-inner-icon="prependInnerIcon"
            :append-icon="appendIcon"
            :append-inner-icon="appendInnerIcon"
            :autocomplete="autocomplete"
            :focused="forceFocusedStyle"
        >
            <template v-if="$slots['default']">
                <slot name="default" v-bind="{ isReadonly }"/>
            </template>
        </v-text-field>
        <v-textarea
            v-else
            @update:model-value="updateModel($event)"
            :model-value="modelValue"
            :class="aInputCustomClass"
            :clearable="clearable"
            :placeholder="placeholder"
            :readonly="readonly"
            :disabled="disabled"
            :prepend-icon="prependIcon"
            :prepend-inner-icon="prependInnerIcon"
            :append-icon="appendIcon"
            :append-inner-icon="appendInnerIcon"
            :auto-grow="autoGrow"
            :row-height="rowHeight"
            :rows="rows"
            :focused="forceFocusedStyle"
        />
        <p class="mb-0" :class="messageClass" v-if="message">{{ message }}</p>
    </div>
</template>

<script lang="ts">

export type AInputSizes = 'x-small' | 'small' | 'medium' | 'large'
export type AInputStatus = 'error' | 'warning' | 'default'
export type AInputTypes = 'textarea' | 'text' | 'password' | 'email' | 'number' | 'tel' | 'url'

</script>

<script setup lang="ts">
import { PropType, defineEmits, defineProps, computed } from 'vue'

const emit = defineEmits(['update:modelValue']);

const props = defineProps({
    label: {
        type: String,
        required: false
    },
    message: {
        type: String,
        required: false
    },
    size: {
        type: String as PropType<AInputSizes>,
        default: 'medium'
    },
    modelValue: {
        required: true
    },
    type: {
        type: String as PropType<AInputTypes>,
        default: 'text'
    },
    status: {
        type: String as PropType<AInputStatus>,
        default: 'default'
    },
    clearable: {
        type: Boolean,
        default: false
    },
    placeholder: {
        type: String,
        required: false
    },
    readonly: {
        type: Boolean,
        default: false
    },
    disabled: {
        type: Boolean,
        default: false
    },
    prependIcon: {
        type: String,
        required: false
    },
    appendIcon: {
        type: String,
        required: false
    },
    prependInnerIcon: {
        type: String,
        required: false
    },
    appendInnerIcon: {
        type: String,
        required: false
    },
    autoGrow: {
        type: Boolean,
        default: false
    },
    rowHeight: {
        type: Number,
        default: 24
    },
    rows: {
        type: Number,
        default: 5
    },
    required: {
        type: Boolean,
        default: false
    },
    autocomplete: {
        type: String,
        required: false
    },
    forceFocusedStyle: {
        type: Boolean,
        required: false
    }
})

const labelMessage = computed(() => {
    if (props.required) {
        return `${props.label} *`
    }
    return props.label
})

const aInputCustomClass = computed(() => {
    const classes = [
        `input-${props.size}`,
        `status-${props.status}`
    ]

    if (props.type === 'textarea') {
        classes.push('textarea')
    }

    return classes
})

const messageClass = computed(() => {
    return [
        `status-${props.status}`
    ]
})

function updateModel(newValue: string) {
    if (props.type === 'number') {
        const numberValue = parseFloat(newValue)
        if (isNaN(numberValue)) {
            emit('update:modelValue', null)
        } else {
            emit('update:modelValue', numberValue)
        }
    } else {
        emit('update:modelValue', newValue)
    }
}

</script>

<style scoped lang="scss">
@mixin input-height($height, $padding-block: 0px){
    height: $height !important;
    
    :deep(.v-field__field) {
        height: $height;
    }
    
    :deep(.v-field__input) {
        padding-block: $padding-block;
        height: $height !important;
        min-height: $height !important;
    }

    :deep(.v-input__prepend), :deep(.v-input__append), :deep(.v-field__prepend-inner), :deep(.v-field__append-inner) {
        padding-block: $padding-block;
        align-items: center;

        svg.v-icon {
            height: $height !important;
            min-height: $height !important;
            margin-block-start: 0px !important;
        }
    }
}

:deep(.v-field__input) {
    padding-left: 8px !important;

    input::placeholder, &::placeholder {
        color: #8c8c8c !important;
        font-family: Karla;
        font-weight: 400;
    }
}

.input-x-small:not(.textarea) {
    @include input-height(30.03px);
}

.input-small:not(.textarea){
    @include input-height(38.04px);
}

.input-medium:not(.textarea){
    @include input-height(46.05px);
}

.input-large:not(.textarea){
    @include input-height(54.02px);
}

.label {
    color: var(--text-color-secondary);
    font-family: Karla;
    font-weight: 400;
    margin-bottom: 4px;
}

:deep(input::-webkit-outer-spin-button),
:deep(input::-webkit-inner-spin-button) {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
:deep(input[type=number]) {
  -moz-appearance: textfield;
}
</style>