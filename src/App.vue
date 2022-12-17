<template>
  <div class="inventory">
    <div class="inventory-idle">
      <div class="inventory__main">
        <div class="inventory__main-info">
          <img src="./assets/info_img.png" alt="">
          <div class="inventory__main-info-bigline"></div>
          <div class="inventory__main-info-section">
            <div class="inventory__main-info-section_box1"></div>
            <div class="inventory__main-info-section_box2"></div>
            <div class="inventory__main-info-section_box3"></div>
            <div class="inventory__main-info-section_box4"></div>
            <div class="inventory__main-info-section_box5"></div>
          </div>
          <div class="inventory__main-info-close"></div>
        </div>
        <div class="inventory__main-board">
          <div v-for="cell in cell" :key="cell.id" @drop="onDrop($event, cell.id)" class="inventory__main-board-list"
            @dragover.prevent @dragenter.prevent>
            <div v-for="item in items.filter(x => x.cellId === cell.id)" @click="optionItem(item)"
              @dragstart="onDragStart($event, item)" class="inventory__main-board-list-box" draggable="true">
              <img src="./assets/board_box.svg" alt="">
              <div class="inventory__main-board-list-box--count">{{ item.count }}</div>
            </div>
          </div>
          <div v-if="isOption" class="inventory__main-board--option"></div>
        </div>
      </div>
      <div class="scroll">
        <div class="scroll__idle"></div>
        <img src="./assets/scroll_img.svg" alt="">
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'App',
  setup() {
    const isOption = false;
    const items = ref([
      {
        id: 0,
        count: '4',
        cellId: 0,
        background: 'red'
      },
      {
        id: 1,
        count: 2,
        cellId: 1
      },
      {
        id: 2,
        count: 5,
        cellId: 2
      },
    ])
    const cell = ref([
      {
        id: 0,
      },
      {
        id: 1,
      },
      {
        id: 2,
      },
      {
        id: 3,
      },
      {
        id: 4,
      },
      {
        id: 5,
      },
      {
        id: 6,
      },
      {
        id: 7,
      },
      {
        id: 8,
      },
      {
        id: 9,
      },
      {
        id: 10,
      },
      {
        id: 11,
      },
      {
        id: 12,
      },
      {
        id: 13,
      },
      {
        id: 14,
      },
      {
        id: 15,
      },
      {
        id: 16,
      },
      {
        id: 17,
      },
      {
        id: 18,
      },
      {
        id: 19,
      },
      {
        id: 20,
      },
      {
        id: 21,
      },
      {
        id: 22,
      },
      {
        id: 23,
      },
      {
        id: 24,
      }
    ])

    function onDragStart(e, item) {
      e.dataTransfer.dropEffect = 'move'
      e.dataTransfer.effectAllowed = 'move'
      e.dataTransfer.setData('itemId', item.id.toString())
    }

    function onDrop(e, cellId) {
      const itemId = parseInt(e.dataTransfer.getData('itemId'))
      items.value = items.value.map(x => {
        if (x.id == itemId)
          x.cellId = cellId
        return x
      })
    }

    function optionItem(item) {
      this.selectedItem = item.count;
      console.log(this.selectedItem);
      console.log(isOption);
      this.isOption = true;
    }

    return {
      items,
      cell,
      onDragStart,
      onDrop,
      optionItem
    }
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #1E1E1E;
}

.inventory {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;

  .inventory-idle {
    display: flex;
    flex-direction: column;
    gap: 24px;

    .inventory__main {
      display: flex;
      justify-content: space-between;

      .inventory__main-info {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 236px;
        height: 500px;
        padding: 18px 14px;
        background: #262626;
        border: 1px solid #4D4D4D;
        border-radius: 12px;

        .inventory__main-info-bigline {
          width: 190px;
          height: 26px;
          margin-top: 20px;
          margin-bottom: 24px;
          background: linear-gradient(90deg, #3C3C3C 0%, #444444 51.04%, #333333 100%);
          border-radius: 8px;
        }

        .inventory__main-info-section {
          display: flex;
          flex-direction: column;
          align-items: center;
          gap: 16px;

          .inventory__main-info-section_box1 {
            width: 155px;
            height: 10px;

            background: linear-gradient(90deg, #3C3C3C 0%, #444444 51.04%, #333333 100%);
            border-radius: 4px;
          }

          .inventory__main-info-section_box2 {
            width: 190px;
            height: 10px;

            background: linear-gradient(90deg, #3C3C3C 0%, #444444 51.04%, #333333 100%);
            border-radius: 4px;
          }

          .inventory__main-info-section_box3 {
            width: 170px;
            height: 10px;

            background: linear-gradient(90deg, #3C3C3C 0%, #444444 51.04%, #333333 100%);
            border-radius: 4px;
          }

          .inventory__main-info-section_box4 {
            width: 160px;
            height: 10px;

            background: linear-gradient(90deg, #3C3C3C 0%, #444444 51.04%, #333333 100%);
            border-radius: 4px;
          }

          .inventory__main-info-section_box5 {
            width: 140px;
            height: 10px;

            background: linear-gradient(90deg, #3C3C3C 0%, #444444 51.04%, #333333 100%);
            border-radius: 4px;
          }
        }

        .inventory__main-info-close {
          width: 80px;
          height: 10px;
          margin-top: 24px;
          background: linear-gradient(90deg, #3C3C3C 0%, #444444 51.04%, #333333 100%);
          border-radius: 4px;
        }
      }

      .inventory__main-board {
        position: relative;
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        grid-template-rows: repeat(5, 1fr);
        background: #262626;
        width: 525px;
        height: 500px;
        border: 1px solid #4D4D4D;
        border-radius: 12px;

        .inventory__main-board-list {
          position: relative;
          border: 1px solid #4D4D4D;
          width: 105px;
          height: 100px;
          display: flex;
          align-items: center;
          justify-content: center;
          cursor: pointer;

          &:first-child {
            border-left: 0px;
            border-top: 0px;
          }

          &:hover {
            background-color: #2F2F2F;
          }

          .inventory__main-board-list-box {
            width: 48px;
            height: 48px;

            &:hover {
              cursor: pointer;
            }

            .inventory__main-board-list-box--count {
              display: flex;
              align-items: center;
              justify-content: center;
              position: absolute;
              bottom: 0;
              right: 0;
              width: 16px;
              height: 16px;

              background: #262626;

              border: 1px solid #4D4D4D;
              border-radius: 6px 0px 0px 0px;
              font-family: 'Inter';
              font-style: normal;
              font-weight: 500;
              font-size: 10px;
              line-height: 12px;
              display: flex;
              align-items: center;
              text-align: center;

              color: #FFFFFF;

              opacity: 0.4;
            }
          }
        }

        .inventory__main-board--option {
          position: absolute;
          width: 250px;
          height: 500px;
          top: 0;
          right: 0;

          background: rgba(38, 38, 38, 0.5);

          border-left: 1px solid #4D4D4D;
          backdrop-filter: blur(8px);
        }
      }
    }

    .scroll {
      position: relative;
      display: flex;
      align-items: center;
      width: 785px;
      height: 72px;

      background: #262626;

      border: 1px solid #4D4D4D;
      border-radius: 12px;

      .scroll__idle {
        margin-left: 18px;
        width: 699px;
        height: 36px;

        background: linear-gradient(90deg, #3C3C3C 0%, #444444 51.04%, #333333 100%);
        border-radius: 12px;
      }

      & img {
        position: absolute;
        right: 1.5%;
        top: 25%;
        cursor: pointer;
      }
    }
  }
}
</style>