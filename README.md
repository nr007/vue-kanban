# vue-kanban

> A drag and drop kanban board component


### Basic Usage

Install the plugin
```js
import vueKanban from 'vue-kanban'

Vue.use(vueKanban)
```

and then use the component in your project.
```html
<kanban-board :stages="stages" :blocks="blocks"></kanban-board>
```

#### Props
- stages: an array of stages for the kanban board
- blocks: an array of objects that will make up the blocks on the kanban board
```js
{
  stages: [
    {
      title: 'kvalificirane priložnosti',
      value: '1.915.800,00 €'
    }, {
      title: 'poslana ponudba',
      value: '1.915.800,00 €'
    }, {
      title: 'v pogajanjih',
      value: '1.915.800,00 €'
    }, {
      title: 'uspešno',
      value: '1.915.800,00 €'
    }, {
      title: 'neuspešno',
      value: '1.915.800,00 €'
    }
  ],
  blocks: [
    {
      id: 1,
      status: 'on-hold',
      title: 'Test',
    }
  ],
}
```

### Receiving Changes
The component will emit an event when a block is moved

```html
<kanban-board :stages="stages" :blocks="blocks" @update-block="updateBlock"></kanban-board>
<script>
...
  methods: {
    updateBlock(id, status) {
      this.blocks.find(b => b.id === Number(id)).status = status;
    },
  },
...
</script>
```

### Add some style
I have included a scss stylesheet in this repo as a starting point that can be used in your project
```html
<style lang="scss">
  @import './assets/kanban.scss';
</style>
```

### Customize the kanban blocks
Each block has a named slot which can be extended from the parent, like so...
```html
<kanban-board :stages="stages" :blocks="blocks" @update-block="updateBlock">
  <div v-for="block in blocks" :slot="block.id">
    <div>
      <strong>id:</strong> {{ block.id }}
    </div>
    <div>
      {{ block.title }}
    </div>
  </div>
</kanban-board>
```
