<script lang="ts">
  import "$lib/main.css";
  import {
    Button,
    Switch,
    Text,
    Card,
    ListItem,
    List,
    Accordion,
    Loading,
    ProgressBar,
    ToolTip,
    Numeric,
    Char,
    RadioElement,
    LongText,
    Modal,
    Table,
    ComboBox,
    ComboBoxElement,
    File,
  } from "$lib/index.js";
  import { writable } from "svelte/store";
  import { onDestroy, onMount } from "svelte";

  let checked = $state(true);
  let value = $state("");
  let numberValue = $state(0);
  let charValue = $state("A");

  let clicked = $state(false);
  let selectMode = $state(false);
  let progress = $state(0);
  let progressDirection = $state(5);

  let ComboBoxList = Array.from({ length: 30 }, (_, i) => `Item ${i + 1}`);
  let ComboBoxListSelected = writable(ComboBoxList[0]);

  let inter: number;

  let modalOpen = $state(false);

  let file = $state<FileList | null | undefined>(null)

  onMount(() => {
    clearInterval(inter);
    inter = setInterval(() => {
      progress = progress + progressDirection;
      if (progress === 105) progressDirection = -5;
      if (progress === -5) progressDirection = 5;
    }, 1000);
  });

  onDestroy(() => {
    clearInterval(inter);
  });

  function onClick() {
    clicked = true;

    setTimeout(() => {
      clicked = false;
    }, 300);
  }

  const items = ["Item 1", "Item 2", "Item 3"];
  $effect(() => {
    console.log(file)
  })
</script>

<div class="groups">
  <div class="groups">
    <div class="group">
      <h2>Button - {clicked}</h2>
      <div class="break"></div>
      <Button primary={false} size="lg" {onClick}>Secondary</Button>
      <Button primary={false} size="lg" active {onClick}>Secondary</Button>
      <Button primary size="md" {onClick}>Primary</Button>
      <Button disabled size="sm" {onClick}>Disabled</Button>
      <Button disabled size="sm" type="danger" {onClick}>Disabled Danger</Button
      >
      <div class="break"></div>
      <Button size="md" type="danger" {onClick}>Danger</Button>
      <Button size="md" type="info" {onClick}>Info</Button>
      <Button size="md" type="success" {onClick}>Sucess</Button>
      <Button size="md" type="warning" {onClick}>Warning</Button>
    </div>
    <div class="group">
      <h2>Switch</h2>
      <div class="break"></div>
      <Switch size="lg" bind:checked>{checked ? "On" : "Off"}</Switch>
      <Switch size="md" bind:checked>{checked ? "On" : "Off"}</Switch>
      <Switch size="sm" bind:checked>{checked ? "On" : "Off"}</Switch>
    </div>
    <div class="group">
      <h2>Numeric</h2>
      <div class="break"></div>
      <Numeric size="lg" bind:value={numberValue} status="danger" />
      <Numeric bind:value={numberValue} status="success" />
      <Numeric bind:value={numberValue} />
      <Numeric size="sm" disabled bind:value={numberValue} status="warning" />
    </div>
    <div class="group">
      <h2>Character - {charValue}</h2>
      <div class="break"></div>
      <Char size="lg" bind:value={charValue} status="danger" />
      <Char status="success" />
      <Char />
      <Char size="sm" max="Z" value={charValue} status="warning" />
    </div>
    <div class="group">
      <h2>File</h2>
      <div class="break"></div>
      <File multiple status="danger" size="lg" bind:file />
      <File disabled size="md" />
      <File multiple status="success" size="sm" />
      <File multiple status="warning" size="sm" />
      <File multiple status="warning" size="sm" hover />
      <File multiple size="sm" selected />
    </div>
    <div class="group">
      <h2>RadioButton</h2>
      <div class="break"></div>
      <RadioElement size="lg" group="group1" value="1">Radio 1</RadioElement>
      <RadioElement size="md" group="group1" value="2">Radio 2</RadioElement>
      <RadioElement size="sm" group="group1" value="3" disabled
        >Radio 3</RadioElement
      >
    </div>
    <div class="group">
      <h2>ComboBox</h2>
      <div class="break"></div>
      <ComboBox size="lg" bind:value={$ComboBoxListSelected}>
        <span slot="selected">{$ComboBoxListSelected}</span>
        <svelte:fragment slot="list">
          {#each ComboBoxList as item}
            <ComboBoxElement value={item} bind:selection={$ComboBoxListSelected}
              >{item}</ComboBoxElement
            >
          {/each}
        </svelte:fragment>
      </ComboBox>
      <ComboBox size="md" bind:value={$ComboBoxListSelected}>
        <span slot="selected">{$ComboBoxListSelected}</span>
        <svelte:fragment slot="list">
          {#each ComboBoxList as item}
            <ComboBoxElement value={item} bind:selection={$ComboBoxListSelected}
              >{item}</ComboBoxElement
            >
          {/each}
        </svelte:fragment>
      </ComboBox>
      <ComboBox size="sm" bind:value={$ComboBoxListSelected}>
        <span slot="selected">{$ComboBoxListSelected}</span>
        <svelte:fragment slot="list">
          {#each ComboBoxList as item}
            <ComboBoxElement value={item} bind:selection={$ComboBoxListSelected}
              >{item}</ComboBoxElement
            >
          {/each}
        </svelte:fragment>
      </ComboBox>
      <ComboBox size="sm" bind:value={$ComboBoxListSelected} disabled>
        <span slot="selected">{$ComboBoxListSelected}</span>
        <svelte:fragment slot="list">
          {#each ComboBoxList as item}
            <ComboBoxElement value={item} bind:selection={$ComboBoxListSelected}
              >{item}</ComboBoxElement
            >
          {/each}
        </svelte:fragment>
      </ComboBox>
    </div>
    <div class="group">
      <h2>Input Text - {value}</h2>
      <div class="break"></div>
      <Text
        placeholder="Placeholder"
        value="Value"
        disabled
        size="lg"
        status="danger"
      />
      <Text placeholder="Placeholder" bind:value size="md" status="success" />
      <Text placeholder="Placeholder" size="sm" bind:value status="warning" />
      <Text placeholder="Placeholder" size="sm" bind:value />
      <Text placeholder="Placeholder" size="sm" bind:value selected />
      <Text placeholder="Placeholder" size="sm" bind:value hover />
    </div>
    <div class="group">
      <h2>Long text - {value}</h2>
      <div class="break"></div>
      <LongText
        placeholder="Placeholder"
        size="lg"
        bind:value
        status="danger"
      />
      <LongText placeholder="Placeholder" bind:value status="success" />
      <LongText
        placeholder="Placeholder"
        size="sm"
        bind:value
        status="warning"
      />
      <LongText placeholder="Placeholder" size="sm" bind:value />
      <LongText placeholder="Placeholder" size="sm" bind:value selected />
      <LongText placeholder="Placeholder" size="sm" bind:value hover />
    </div>
  </div>

  <div class="group">
    <h2>Accordion</h2>
    <div class="break"></div>
    <Accordion status="danger" size="lg" disabled>
      <svelte:fragment slot="title">Title</svelte:fragment>
      <span
        >Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis
        animi dignissimos fugiat provident tempora deleniti eligendi ducimus
        fugit, minus ullam? Tempora dolor illo consectetur deleniti nesciunt
        architecto minus omnis.
      </span>
    </Accordion>
    <Accordion status="success" size="md">
      <svelte:fragment slot="title">Title</svelte:fragment>
      <span
        >Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis
        animi dignissimos fugiat provident tempora deleniti eligendi ducimus
        fugit, minus ullam? Tempora dolor illo consectetur deleniti nesciunt
        architecto minus omnis.
      </span>
    </Accordion>
    <Accordion status="warning" size="sm" hover>
      <svelte:fragment slot="title">Title</svelte:fragment>
      <span
        >Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis
        animi dignissimos fugiat provident tempora deleniti eligendi ducimus
        fugit, minus ullam? Tempora dolor illo consectetur deleniti nesciunt
        architecto minus omnis.
      </span>
    </Accordion>
    <Accordion size="sm">
      <svelte:fragment slot="title">Title</svelte:fragment>
      <span
        >Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis
        animi dignissimos fugiat provident tempora deleniti eligendi ducimus
        fugit, minus ullam? Tempora dolor illo consectetur deleniti nesciunt
        architecto minus omnis.
      </span>
    </Accordion>
    <Accordion size="sm" selected>
      <svelte:fragment slot="title">Title</svelte:fragment>
      <span
        >Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis
        animi dignissimos fugiat provident tempora deleniti eligendi ducimus
        fugit, minus ullam? Tempora dolor illo consectetur deleniti nesciunt
        architecto minus omnis.
      </span>
    </Accordion>
  </div>

  <div class="group">
    <h2>
      List/CheckBox - <Button onClick={() => (selectMode = !selectMode)}
        >{selectMode ? "List" : "Selction"}</Button
      >
    </h2>
    <div class="break"></div>
    <List bind:checkbox={selectMode} let:checkbox let:parentChecked>
      <ListItem size="sm" {checkbox} {parentChecked}>
        First
        <svelte:fragment slot="at">18:40</svelte:fragment>
        <svelte:fragment slot="subtitle">Subtitle</svelte:fragment>
        <svelte:fragment slot="content"
          >Lorem ipsum dolor sit amet, consectetur adipisicing elit. Libero
          tenetur tempore dolores facilis, ipsum porro, consequatur.</svelte:fragment
        >
      </ListItem>
      <ListItem size="sm" {checkbox} {parentChecked}>Second</ListItem>
    </List>
  </div>

  <div class="group">
    <h2>Card</h2>
    <div class="break"></div>
    <Card size="sm" aspect="" status="danger" hover={true}>
      <svelte:fragment slot="title">Header</svelte:fragment>
      <svelte:fragment>
        <span
          >Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis
          animi dignissimos fugiat provident tempora deleniti eligendi ducimus
          fugit, minus ullam? Tempora dolor illo consectetur deleniti nesciunt
          architecto minus omnis.</span
        >
      </svelte:fragment>
      <svelte:fragment slot="footer">Footer</svelte:fragment>
    </Card>
    <Card size="sm" status="success">
      <svelte:fragment slot="title">Header</svelte:fragment>
      <svelte:fragment slot="legend">legend</svelte:fragment>
      <svelte:fragment>
        <span
          >Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis
          animi dignissimos fugiat provident tempora deleniti eligendi ducimus
          fugit, minus ullam? Tempora dolor illo consectetur deleniti nesciunt
          architecto minus omnis.</span
        >
      </svelte:fragment>
      <svelte:fragment slot="footer">Footer</svelte:fragment>
    </Card>
    <Card size="lg" status="warning">
      <span
        >Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis
        animi dignissimos fugiat provident tempora deleniti eligendi ducimus
        fugit, minus ullam? Tempora dolor illo consectetur deleniti nesciunt
        architecto minus omnis.
      </span>
    </Card>
    <Card size="lg">
      <span
        >Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis
        animi dignissimos fugiat provident tempora deleniti eligendi ducimus
        fugit, minus ullam? Tempora dolor illo consectetur deleniti nesciunt
        architecto minus omnis.
      </span>
    </Card>
    <Card size="lg" selected>
      <span
        >Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis
        animi dignissimos fugiat provident tempora deleniti eligendi ducimus
        fugit, minus ullam? Tempora dolor illo consectetur deleniti nesciunt
        architecto minus omnis.
      </span>
    </Card>
  </div>

  <div class="group">
    <h2>Gauge</h2>
    <div class="break"></div>
    <Loading show={true} showText={false} size="lg" />
    <Loading show={true} showText={true} size="md" />
    <Loading show={true} showText={true} size="sm">Custom</Loading>
    <div class="break"></div>
    <h2>Progress Bar</h2>
    <div class="break"></div>
    <ProgressBar value={50} />
    <ProgressBar value={75} />
    <ProgressBar value={progress} />
  </div>

  <div class="group">
    <h2>Tooltip</h2>
    <div class="break"></div>
    <span>
      Lorem ipsum dolor,<ToolTip>
        <span class="tooltip">Lorem ipsum dolor,Lorem ipsum dolor</span
        ></ToolTip
      >
      sit amet consectetur adipisicing elit. Doloribus minus est a facilis alias
      laborum
    </span>
  </div>

  <div class="group">
    <h2 class="v-align">
      Modal - <Button size="md" onClick={() => (modalOpen = !modalOpen)}
        >Open</Button
      >
    </h2>
    <div class="break"></div>
    <Modal bind:state={modalOpen}>
      <svelte:fragment slot="title">Title</svelte:fragment>
      <span
        >Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe omnis
        animi dignissimos fugiat provident tempora deleniti eligendi ducimus
        fugit, minus ullam? Tempora dolor illo consectetur deleniti nesciunt
        architecto minus omnis.
      </span>
    </Modal>
  </div>
  <div class="group">
    <h2>Table</h2>
    <div class="break"></div>
    <Table>
      <thead>
        <tr>
          <th>Header 1</th>
          <th>Header 2</th>
          <th>Header 3</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Row 1</td>
          <td>Row 1</td>
          <td>Row 1</td>
        </tr>
        <tr>
          <td>Row 2</td>
          <td>Row 2</td>
          <td>Row 2</td>
        </tr>
        <tr>
          <td>Row 3</td>
          <td>Row 3</td>
          <td>Row 3</td>
        </tr>
      </tbody>
    </Table>
  </div>
</div>

<style>
  .groups {
    display: flex;
    flex-direction: column;
    width: 100%;
  }
  .group {
    margin: 0 20px;
    display: flex;
    flex-direction: row;
    gap: 0.25rem 0.5rem;
    flex-wrap: wrap;
    padding-bottom: 1.5em;
    margin-bottom: 1rem;
    align-items: start;
  }
  .group {
    border-bottom: 1px solid var(--border-color);
  }
  .break {
    flex-basis: 100%;
    width: 0;
  }
  h2 {
    padding-bottom: 0.5rem;
    font-size: 1.4rem;
    color: var(--pure);
  }

  .v-align {
    display: flex;
    gap: 0.5rem;
  }

  .tooltip {
    width: 200px;
  }
</style>
