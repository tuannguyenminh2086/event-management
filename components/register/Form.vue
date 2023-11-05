<template>
  <div>
    <UContainer>
        <UForm ref="form" :schema="schema" :state="state" @submit="onSubmit">

          <div class="grid grid-cols-12 gap-5 gap-y-10 mb-10">
            <div class="col-span-full">
              <URadioGroup 
                :options="titles"
                v-model="state.title"
              />
            </div>
            <div class="col-span-full lg:col-span-6">
              <UFormGroup label="First Name" name="firstName">
                <UInput v-model="state.firstName" size="lg"/>
              </UFormGroup>
            </div>
            <div class="col-span-full lg:col-span-6">
              <UFormGroup label="Last Name" name="lastName">
                <UInput v-model="state.lastName" size="lg" />
              </UFormGroup>
            </div>
            <div class="col-span-full lg:col-span-6">
              <UFormGroup label="Job title" name="jobTitle">
                <UInput v-model="state.jobTitle"  size="lg" />
              </UFormGroup>
            </div>
            <div class="col-span-full lg:col-span-6">
              <UFormGroup label="Company" name="company">
                <UInput v-model="state.company" size="lg" />
              </UFormGroup>
            </div>
            <div class="col-span-full lg:col-span-6">
              <UFormGroup label="Email" name="email">
                <UInput v-model="state.email" type="email" size="lg" />
              </UFormGroup>
            </div>
            <div class="col-span-full lg:col-span-6">
              <UFormGroup label="Phone number" name="phone">
                <UInput v-model="state.phone" size="lg" />
              </UFormGroup>
            </div>

          </div>
          

          <UButton type="submit" size="lg" loading>
            Submit
          </UButton>
          
        </UForm>
      </UContainer>
  </div>
</template>

<script setup lang="ts">
  import { z } from 'zod'
  import type { FormError, FormSubmitEvent } from '#ui/types'

  const schema = z.object({
    firstName: z.string().min(2, 'Must be at least 2 characters'),
    lastName: z.string().min(2, 'Must be at least 2 characters'),
    title: z.string().optional(),
    jobTitle: z.string().optional(),
    company: z.string().optional(),
    email: z.string().email('Invalid email'),
    phone: z.string().optional()
  })

  type Schema = z.output<typeof schema>

  const state = reactive({
    firstName: undefined,
    lastName: undefined,
    title:  undefined,
    jobTitle: undefined,
    company: undefined,
    email: undefined,
    phone: undefined
  })

  const titles = [
    { value: 'mr', label: 'Mr.' },
    { value: 'ms/mrs', label: 'Ms./Mrs.' }
  ]

  const form = ref()

  async function onSubmit (event: FormSubmitEvent<Schema>) {
    // Do something with data
    console.log(event.data)
  }

</script>

<style scoped>

</style>