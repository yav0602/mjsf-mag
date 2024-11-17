<template>
  <div class="space-y-4 p-6">
    <h2 class="text-2xl font-bold mb-4">Демо компонента кнопки</h2>
    <div>
      <h3 class="text-lg font-semibold mb-2">Кольори</h3>
      <div class="space-x-2">
        <Button
          label="Червона кнопка"
          color="red"
          size="medium"
          icon="🔥"
          @click="handleClick('Червона кнопка')"
        />
        <Button
          label="Зелена кнопка"
          color="green"
          size="medium"
          icon="🌿"
          @click="handleClick('Зелена кнопка')"
        />
        <Button
          label="Синя кнопка"
          color="blue"
          size="medium"
          icon="💧"
          @click="handleClick('Синя кнопка')"
        />
      </div>
    </div>
    <div>
      <h3 class="text-lg font-semibold mb-2">Розміри</h3>
      <div class="space-x-2">
        <Button
          label="Маленька кнопка"
          color="blue"
          size="small"
          icon="🔹"
          @click="handleClick('Маленька кнопка')"
        />
        <Button
          label="Середня кнопка"
          color="blue"
          size="medium"
          icon="🔷"
          @click="handleClick('Середня кнопка')"
        />
        <Button
          label="Велика кнопка"
          color="blue"
          size="large"
          icon="🔵"
          @click="handleClick('Велика кнопка')"
        />
      </div>
    </div>
    <div>
      <h3 class="text-lg font-semibold mb-2">Пошуковий випадаючий список</h3>
      <SearchableDropdown
        :items="dropdownItems"
        @select="handleDropdownSelect"
      />
    </div>
    <div>
      <h3 class="text-lg font-semibold mb-2">Пошуковий випадаючий список з вибором декількох елементів</h3>
      <SearchableDropdown :items="dropdownItems" @select="handleDropdownSelect" :multiple="true" />
    </div>
  </div>
</template>

<script>
import Button from "./components/Button.vue";
import SearchableDropdown from './components/SearchableDropdown.vue';

export default {
  name: "App",
  components: {
    Button,
    SearchableDropdown,
  },
  data() {
    return {
      dropdownItems: [
        { label: "Опція 1", icon: "🌟" },
        { label: "Опція 2", icon: "🔥" },
        { label: "Опція 3", icon: "💧" },
        { label: "Опція 4", icon: "🍀" },
      ],
    };
  },
  methods: {
    handleClick(buttonLabel) {
      console.log(`${buttonLabel} натиснуто!`);
    },
    handleDropdownSelect(item) {
      if (item) {
        console.log(`Вибрано: ${item.label}`);
      } else {
        console.log("Вибір очищено");
      }
    },
  },
};
</script>

<style scoped></style>
