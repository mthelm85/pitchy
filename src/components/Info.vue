<template>
    <transition name="modal">
        <div class="modal-mask">
            <div class="modal-wrapper">
            <div class="modal-container">
                <div class="modal-header">
                <slot name="header">
                    How To Use Pitchy
                </slot>
                </div>

                <div class="modal-body">
                <slot name="body">
                    <ul>
                        <li><strong>Double-click</strong> to add a player to the pitch</li>
                        <li><strong>C</strong> to change color</li>
                        <li><strong>D</strong> to switch to drawing mode</li>
                        <li><strong>E</strong> to edit player name/number</li>
                        <li><strong>G</strong> to group objects</li>
                        <li><strong>I</strong> to display instructions</li>
                        <li><strong>U</strong> to ungroup objects</li>
                        <li><strong>Delete</strong> to remove a player/marking from the pitch</li>
                    </ul>

                    You can select multiple objects by holding <strong>Shift</strong> or by clicking & dragging with the mouse
                </slot>
                </div>

                <div class="modal-footer">
                <slot name="footer">
                    © {{ new Date().getFullYear() }} Pitchy
                    <button class="button modal-default-button" @click="$emit('close')">
                    OK
                    </button>
                </slot>
                </div>
            </div>
            </div>
        </div>
    </transition>
</template>
<script>

</script>
<style scoped>
.button:active {
    box-shadow: 7px 6px 28px 1px rgba(0, 0, 0, 0.24);
    transform: translateY(4px);
    /* Moving button 4px to y-axis */
}

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 6px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
  text-align: justify;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 8px 16px;
  text-align: center;
  text-decoration: none;
  font-size: 12px;
  margin: 4px 2px;
  transition-duration: 0.4s;
  cursor: pointer;
  border-radius: 6px;;
  float: right;
}

/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>