<template>
  <div>
    <nav class="ml-6">
      <ul class="flex space-x-4 list-inside list-disc">
        <li>
          <Link
            href="/"
            class="text-blue-500 hover:underline"
            :class="{ 'font-bold underline': $page.url === '/' }"
            >Home</Link
          >
        </li>
        <li>
          <Link href="/users" class="text-blue-500 hover:underline" :class="{ 'font-bold underline': $page.url.startsWith('/users') }">Users</Link>
        </li>
        <li>
          <Link href="/settings" class="text-blue-500 hover:underline" :class="{ 'font-bold underline': $page.url === '/settings' }"
            >Settings</Link
          >
        </li>
        <li>
          <Link
            href="/logout"
            method="post"
            :data="{ foo: 'bar' }"
            as="button"
            class="text-blue-500 hover:underline"
            >log out</Link
          >
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {};
</script>