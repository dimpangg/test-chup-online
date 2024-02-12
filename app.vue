<script setup lang="ts">
import IconDotsThree from "~/assets/icon-dots-three.svg";

type Response = {
  products: Product[];
  total: number;
  skip: number;
  limit: number;
};

type Product = {
  id: number;
  title: string;
  price: number;
  brand: string;
  stock: number;
};

const skip = ref(0);
const q = ref("");

const url = computed(() =>
  q.value ? `https://dummyjson.com/products/search` : `https://dummyjson.com/products`
);

const { data, pending, error, refresh } = await useFetch<Response>(url, {
  query: {
    limit: 10,
    skip,
    select: "title,price,brand,stock",
    q,
  },
});

const onNext = () => {
  skip.value += 10;
};
const onPrev = () => {
  skip.value -= 10;
};
</script>

<template>
  <div>
    <div class="bg-slate-100 flex flex-col gap-2 p-6">
      Button Medium
      <div class="flex gap-2">
        <Button>Click me</Button>
        <Button intent="secondary">Click Second</Button>
        <Button intent="tertiary">Click Third</Button>
        <Button intent="dashed">Click Dashed</Button>
        <Button intent="link">Link</Button>
        <Button intent="text">Text</Button>
      </div>
    </div>
    <div class="bg-slate-100 flex flex-col gap-2 p-6">
      Button Large
      <div class="flex gap-2">
        <Button size="large">Click me</Button>
        <Button intent="secondary" size="large">Click Second</Button>
        <Button intent="tertiary" size="large">Click Third</Button>
        <Button intent="dashed" size="large">Click Dashed</Button>
        <Button intent="link" size="large">Link</Button>
        <Button intent="text" size="large">Text</Button>
      </div>
    </div>
    <div class="bg-slate-100 flex flex-col gap-2 p-6">
      Button Small
      <div class="flex gap-2">
        <Button size="small">Click me</Button>
        <Button intent="secondary" size="small">Click Second</Button>
        <Button intent="tertiary" size="small">Click Third</Button>
        <Button intent="dashed" size="small">Click Dashed</Button>
        <Button intent="link" size="small">Link</Button>
        <Button intent="text" size="small">Text</Button>
      </div>
    </div>
    <div class="bg-slate-100 flex flex-col gap-2 p-6">
      <span class="underline">Input</span>
      <div class="flex gap-2">
        <InputWrapper label="Input Large">
          <Input placeholder="Text Here" size="large" />
        </InputWrapper>
        <InputWrapper label="Input Medium">
          <Input placeholder="Text Here" />
        </InputWrapper>
        <InputWrapper label="Input Small">
          <Input placeholder="Text Here" size="small" disabled />
        </InputWrapper>
      </div>
    </div>
    <div class="bg-slate-100 flex flex-col gap-2 p-6">
      <span class="underline">Table</span>
      <Table>
        <thead>
          <tr>
            <Th withSort>Name</Th>
            <Th withSort>Name 1</Th>
            <Th withSort>Name 1</Th>
            <Th></Th>
          </tr>
        </thead>
        <tbody>
          <Tr>
            <Td>Test</Td>
            <Td>Test</Td>
            <Td>Test</Td>
            <Td><IconDotsThree class="text-[#343330]" /></Td>
          </Tr>
          <Tr>
            <Td>Test</Td>
            <Td>Test</Td>
            <Td>Test</Td>
            <Td><IconDotsThree class="text-[#343330]" /></Td>
          </Tr>
          <Tr>
            <Td>Test</Td>
            <Td>Test</Td>
            <Td>Test</Td>
            <Td><IconDotsThree class="text-[#343330]" /></Td>
          </Tr>
          <Tr>
            <Td>Test</Td>
            <Td>Test</Td>
            <Td>Test</Td>
            <Td><IconDotsThree class="text-[#343330]" /></Td>
          </Tr>
        </tbody>
      </Table>
    </div>

    <div class="bg-slate-100 flex flex-col gap-2 p-6 my-12">
      <span class="underline">Test API</span>
      <div class="flex flex-col gap-10">
        <div class="ml-auto">
          <Input placeholder="Search" v-model="q" />
        </div>
        <div>
          <Table>
            <thead>
              <tr>
                <Th withSort>Title</Th>
                <Th withSort>Brand</Th>
                <Th withSort>Price</Th>
                <Th>Stock</Th>
              </tr>
            </thead>
            <tbody>
              <Tr v-for="(item, i) in data?.products" :key="item.id">
                <Td>{{ item.title }}</Td>
                <Td>{{ item.brand }}</Td>
                <Td>{{
                  Intl.NumberFormat("en-US", {
                    style: "currency",
                    currency: "USD",
                  }).format(item.price)
                }}</Td>
                <Td>{{ item.stock }}</Td>
              </Tr>
            </tbody>
          </Table>
        </div>
        <div class="ml-auto flex gap-4">
          <Button :disabled="skip === 0" @click="onPrev">Prev</Button>
          <Button :disabled="skip === 90 || data?.limit === data?.total" @click="onNext"
            >Next</Button
          >
        </div>
      </div>
    </div>
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500&display=swap");

html {
  font-family: "Poppins", sans-serif;
}
</style>
