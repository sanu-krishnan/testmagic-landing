<script setup lang="ts">
const faqs = [
    {
        question: "What really is TestMagic?",
        answer:
            "TestMagic is your AI-powered API testing buddy. Give it your Swagger or OpenAPI documentation, and it will generate test cases, run them, fix them, and even help maintain them—without you writing a single line of test code (unless you want to!).",
    },
    {
        question: "How do I get started?",
        answer:
            "Just paste your API’s Swagger/OpenAPI link on the dashboard, hit 'Connect', and you're off to the races! TestMagic will analyze your endpoints and start generating test cases instantly.",
    },
    {
        question: "What types of tests are generated?",
        answer:
            "TestMagic creates Functional, Validation, and Boundary tests—all written in clean, readable Mocha/Chai syntax.",
    },
    {
        question: "Can I edit or customize the tests?",
        answer:
            "Absolutely! You can edit manually, use AI suggestions, or let TestMagic auto-fix tests based on real API responses. You’re always in control.",
    },
    {
        question: "Does it support multiple environments?",
        answer:
            "Yes! You can create and manage multiple environments with base URLs, bearer tokens, and custom headers.",
    },
    {
        question: "Is my API data secure?",
        answer:
            "Yes! We don’t store your actual API responses or payloads.",
    },
    {
        question: "Do I need to install anything?",
        answer:
            "Nope! It runs right in your browser. No npm installs, no CLI tools. Just plug in your API and go.",
    },
    {
        question: "How does the AI 'fix' broken tests?",
        answer:
            "It inspects the API response, identifies mismatches, and fixes.",
    },
    {
        question: "Will this work with my CI/CD?",
        answer:
            "Not yet—but it’s coming! We're building CLI + CI/CD support so you can run tests automatically in your pipeline.",
    },
    {
        question: "Is it free? What are the plans?",
        answer:
            "TestMagic is free during our beta phase. We'll introduce affordable pricing soon—with a generous free tier.",
    },
    {
        question: "Can I give feedback or request features?",
        answer:
            "Please do! We love hearing from you. Email us at sanu@testmagic.io",
    },
];
</script>

<template>
    <section class="w-full max-w-2xl mx-auto px-4 py-12">
        <h2 class="text-2xl sm:text-3xl md:text-4xl font-medium text-center mb-3 sm:mb-8">Frequently Asked Questions
        </h2>
        <div class="space-y-1">
            <details v-for="(faq, index) in faqs" :key="index"
                class="border rounded-xl shadow-sm bg-background/70 overflow-hidden">
                <summary class="px-5 py-4 cursor-pointer text-base hover:border-primary hover:text-primary">
                    {{ faq.question }}
                </summary>
                <div class="px-5 -mt-2 pb-6 opacity-85">
                    {{ faq.answer }}
                </div>
            </details>
        </div>
    </section>
</template>

<style scoped></style>