<script setup>
const props = defineProps(['moduloCalculo', 'filtraCalculo', 'estado1', 'estado2']);
const emit = defineEmits(['atualiza-numero1', 'atualiza-numero2']);
</script>
<template>
    <form @submit.prevent="props.moduloCalculo">
        <div class="col-md-2 mb-3">
            <select @change="props.filtraCalculo" class="form-control">
                <option value="soma">Soma</option>
                <option value="subtracao">Subtração</option>
                <option value="multiplicacao">Multiplicação</option>
                <option value="divisao">Divisão</option>
            </select>
        </div>
        <div class="row">
            <div class="col">
                <input :value="props.estado1" @input="emit('atualiza-numero1', $event.target.value)" required
                    type="number" class="form-control" placeholder="Digite um número" />
            </div>
            <div class="col">
                <input :value="props.estado2" @input="emit('atualiza-numero2', $event.target.value)" required
                    type="number" class="form-control" placeholder="Digite outro número" />
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Calcular</button>
            </div>
        </div>
    </form>
</template>