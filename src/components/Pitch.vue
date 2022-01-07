<template>
  <canvas id="pitch-canvas" class="pitch-canvas"></canvas>
</template>
<script>
import { fabric } from 'fabric';

export default {
  name: 'Pitch',
  data () {
    return {
      canvas: null,
      colors: ['#DA291C','#6C1D45','#034694','#6CABDD','#c9bc00','#11210C'],
      current: 1,
      draw: false
    }
  },

  mounted () {
    this.canvas = new fabric.Canvas('pitch-canvas', {
      width: 800,
      height: 1100
    })
    fabric.Image.fromURL('./pitch.png', img => {
      this.canvas.setBackgroundImage(img, this.canvas.renderAll.bind(this.canvas), {
        scaleX: this.canvas.width / img.width,
        scaleY: this.canvas.height / img.height
      })
    })
    this.canvas.on('mouse:dblclick', e => {
      let pointer = this.canvas.getPointer(e.e)
      let posX = pointer.x
      let posY = pointer.y
      let circ = new fabric.Circle({
        radius: 25,
        originX: 'center',
        originY: 'center',
        fill: '#DA291C',
      })
      let label = new fabric.IText('Name\n#', {
        fontSize: 12,
        originX: 'center',
        originY: 'center',
        fontFamily: 'Arial',
        textAlign: 'center',
        fill: 'white'
      })
      let group = new fabric.Group([circ, label], {
        left: posX - 25,
        top: posY - 25
      })
      circ.hasControls = false
      label.hasControls = false
      group.hasControls = false
      this.canvas.add(group)
    })
    window.onkeydown = this.keyCommand
  },

  methods: {
    keyCommand (e) {
      switch (e.keyCode) {
        case 46: {
            this.remove()
            break
        }
        case 68: {
          this.drawSwitch()
          break
        }
        case 69: {
          this.edit()
          break
        }
        case 71: {
          this.group()
          break
        }
        case 67: {
          this.changeColor()
          break
        }
        case 85: {
          this.ungroup()
          break
        }
      }
    },

    changeColor () {
      let activeObjects = this.canvas.getActiveObjects()
      activeObjects.forEach(obj => {
        let objects = obj.getObjects()
        objects.forEach(obj => {
          if (obj.get('type') == 'circle') { obj.set('fill', this.colors[this.current]) }
        })
      })
      this.current == 5 ? this.current = 0 : this.current += 1
      this.canvas.renderAll()
    },

    drawSwitch () {
      if (this.canvas.getActiveObject() == undefined) {
        this.draw = !this.draw
        this.canvas.isDrawingMode = this.draw
      }
    },

    edit () {
      let g = this.canvas.getActiveObject()
      let items = g._objects
      g._restoreObjectsState()
      this.canvas.remove(g)
      for (let i = 0; i < items.length; i++) {
        items[i].hasControls = false
        this.canvas.add(items[i])
      }
      this.canvas.setActiveObject(items[1])
      items[1].on('editing:exited', () => {
        let group = new fabric.Group(items)
        group.hasControls = false
        this.canvas.add(group)
      })
      this.canvas.renderAll()

    },

    ungroup () {
      let g = this.canvas.getActiveObject()
      let items = g._objects
      g._restoreObjectsState()
      this.canvas.remove(g)
      for (let i = 0; i < items.length; i++) {
        items[i].hasControls = false
        this.canvas.add(items[i])
      }
      this.canvas.renderAll()
    },

    group () {
      let g = this.canvas.getActiveObject().toGroup()
      g.hasControls = false
      this.canvas.requestRenderAll()
    },

    remove () {
      let activeObjects = this.canvas.getActiveObjects()
      activeObjects.forEach(obj => this.canvas.remove(obj))
      this.canvas.renderAll()
    }
  }
}
</script>

<style scoped>
.pitch-canvas {
  height: 95vh;
  width: 100vh;
  position: relative;
}

.pitch-img {
  height: 95vh;
  width: 100vh;
  position: absolute;
}

.pitch-parent {
    display: inline-block;
    width: 100vh; 
    height: 95vh;
    position: relative;
    margin: 0 auto;
}
</style>