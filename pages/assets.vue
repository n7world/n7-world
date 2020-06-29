<template lang="pug">
  v-container
    // PDF of Rules
    h2.display-1.mt-10.mb-3 Player's Manual PDF
    v-btn(to="/print/pdf" color="primary") View

    hr.my-10

    h2.display-1 Character Sheets, Roll20 Assets, and other things

    ul
      li
        a(href="https://drive.google.com/drive/u/0/folders/10S3R_Tfi4bJ9X2b6-4OI65m9F8fx6i0P" target="_blank") All N7.World Assets
      li
        a(href="https://drive.google.com/drive/folders/1RsYfHzmvv-md8_dIrQU65LpWzTr0kpCR?usp=sharing" target="_blank") Character Sheets
      li
        a(href="https://drive.google.com/drive/folders/1IbS1Rgym6vUjA9ntYgYMmit7dzhANoaI?usp=sharing" target="_blank") Roll20 Sheets & Tokens
      li
        a(href="https://drive.google.com/drive/folders/1MJCLI665gTVni_swC2tMUd1cv8GILF0u?usp=sharing" target="_blank") Premade Characters
      li
        a(href="https://drive.google.com/drive/folders/1WpR2M9CpNKKRYTS_Gzi3Woq8NscRkxOY?usp=sharing" target="_blank") Other items (spell card box, equipment sheets, etc.)

    v-alert(:value="true" type="info").mt-3.
      Please note that you have view-only access to these documents. If you would like to edit a document (such as using a character sheet for your
      own character), you will need to make a copy of the document: #[strong File > Make a copy]. If that option is greyed out, you need to sign
      into your google account to make a copy in your personal Google Drive.

    hr.my-10

    // Spell Cards
    h2.display-1.mb-3 Spell Cards
    v-btn(to="/print/spell-cards" color="primary") View
</template>

<script>

export default {
  head () {
    return {
      title: 'Assets | N7 World'
    }
  }
}
</script>
