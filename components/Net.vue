<template>
  <section>
    <h2>展開図ルービックキューブ</h2>
    <button @click="rotate(1)">左回転</button>
    <!--<button @click="rotate(-1)">右回転</button>-->
    <svg viewBox="-1 -1 200 200">
      <g @click="select(i)" class="inline" v-for="(face, i) in rubikCube" :key="i">
        <g v-for="(row, j) in face" :key="i + ',' + j">
          <rect
            :x="points[i][j][k][0]"
            :y="points[i][j][k][1]"
            width="10"
            height="10"
            v-for="(bg, k) in row"
            :key="i + ',' + j + ',' + k"
            :fill="colors[bg]"
            stroke-width="1"
            :stroke="selected[i] ? 'lightgreen':'gray'"
          ></rect>
        </g>
      </g>
    </svg>
  </section>
</template>
<script>
export default {
  data() {
    return {
      selected: [1, 0, 0, 0, 0, 0],
      points: [
        [
          [[30, 0], [40, 0], [50, 0]],
          [[30, 10], [40, 10], [50, 10]],
          [[30, 20], [40, 20], [50, 20]]
        ],
        [
          [[0, 30], [10, 30], [20, 30]],
          [[0, 40], [10, 40], [20, 40]],
          [[0, 50], [10, 50], [20, 50]]
        ],
        [
          [[30, 30], [40, 30], [50, 30]],
          [[30, 40], [40, 40], [50, 40]],
          [[30, 50], [40, 50], [50, 50]]
        ],
        [
          [[60, 30], [70, 30], [80, 30]],
          [[60, 40], [70, 40], [80, 40]],
          [[60, 50], [70, 50], [80, 50]]
        ],
        [
          [[30, 60], [40, 60], [50, 60]],
          [[30, 70], [40, 70], [50, 70]],
          [[30, 80], [40, 80], [50, 80]]
        ],
        [
          [[30, 90], [40, 90], [50, 90]],
          [[30, 100], [40, 100], [50, 100]],
          [[30, 110], [40, 110], [50, 110]]
        ]
      ],
      colors: ["orange", "white", "green", "yellow", "red", "blue"],
      rubikCube: [
        [[0, 0, 0], [0, 0, 0], [0, 0, 0]],
        [[1, 1, 1], [1, 1, 1], [1, 1, 1]],
        [[2, 2, 2], [2, 2, 2], [2, 2, 2]],
        [[3, 3, 3], [3, 3, 3], [3, 3, 3]],
        [[4, 4, 4], [4, 4, 4], [4, 4, 4]],
        [[5, 5, 5], [5, 5, 5], [5, 5, 5]]
      ]
    };
  },
  methods: {
    rotate(direction) {
      var copy = JSON.parse(JSON.stringify(this.rubikCube));
      if (this.selected[0]) {
        if (direction === 1) {
          // orange
          this.rubikCube[0][0][0] = copy[0][0][2];
          this.rubikCube[0][0][1] = copy[0][1][2];
          this.rubikCube[0][0][2] = copy[0][2][2];
          this.rubikCube[0][1][0] = copy[0][0][1];

          this.rubikCube[0][1][2] = copy[0][2][1];
          this.rubikCube[0][2][0] = copy[0][0][0];
          this.rubikCube[0][2][1] = copy[0][1][0];
          this.rubikCube[0][2][2] = copy[0][2][0];

          this.rubikCube[1][0][0] = copy[5][2][2];
          this.rubikCube[1][0][1] = copy[5][2][1];
          this.rubikCube[1][0][2] = copy[5][2][0];

          this.rubikCube[2][0][0] = copy[1][0][0];
          this.rubikCube[2][0][1] = copy[1][0][1];
          this.rubikCube[2][0][2] = copy[1][0][2];

          this.rubikCube[3][0][0] = copy[2][0][0];
          this.rubikCube[3][0][1] = copy[2][0][1];
          this.rubikCube[3][0][2] = copy[2][0][2];

          this.rubikCube[5][2][0] = copy[3][0][2];
          this.rubikCube[5][2][1] = copy[3][0][1];
          this.rubikCube[5][2][2] = copy[3][0][0];
        } else if (direction === -1) {
        }
      } else if (this.selected[1]) {
        if (direction === 1) {
          // white
          this.rubikCube[1][0][0] = copy[1][0][2];
          this.rubikCube[1][0][1] = copy[1][1][2];
          this.rubikCube[1][0][2] = copy[1][2][2];
          this.rubikCube[1][1][0] = copy[1][0][1];

          this.rubikCube[1][1][2] = copy[1][2][1];
          this.rubikCube[1][2][0] = copy[1][0][0];
          this.rubikCube[1][2][1] = copy[1][1][0];
          this.rubikCube[1][2][2] = copy[1][2][0];

          this.rubikCube[0][0][0] = copy[2][0][0];
          this.rubikCube[0][1][0] = copy[2][1][0];
          this.rubikCube[0][2][0] = copy[2][2][0];

          this.rubikCube[2][0][0] = copy[4][0][0];
          this.rubikCube[2][1][0] = copy[4][1][0];
          this.rubikCube[2][2][0] = copy[4][2][0];

          this.rubikCube[4][0][0] = copy[5][0][0];
          this.rubikCube[4][1][0] = copy[5][1][0];
          this.rubikCube[4][2][0] = copy[5][2][0];

          this.rubikCube[5][0][0] = copy[0][0][0];
          this.rubikCube[5][1][0] = copy[0][1][0];
          this.rubikCube[5][2][0] = copy[0][2][0];
        }
      } else if (this.selected[2]) {
        if (direction === 1) {
          // green
          this.rubikCube[2][0][0] = copy[2][0][2];
          this.rubikCube[2][0][1] = copy[2][1][2];
          this.rubikCube[2][0][2] = copy[2][2][2];
          this.rubikCube[2][1][0] = copy[2][0][1];

          this.rubikCube[2][1][2] = copy[2][2][1];
          this.rubikCube[2][2][0] = copy[2][0][0];
          this.rubikCube[2][2][1] = copy[2][1][0];
          this.rubikCube[2][2][2] = copy[2][2][0];

          this.rubikCube[0][2][0] = copy[3][0][0];
          this.rubikCube[0][2][1] = copy[3][1][0];
          this.rubikCube[0][2][2] = copy[3][2][0];

          this.rubikCube[1][0][2] = copy[0][2][2];
          this.rubikCube[1][1][2] = copy[0][2][1];
          this.rubikCube[1][2][2] = copy[0][2][0];

          this.rubikCube[4][0][0] = copy[1][0][2];
          this.rubikCube[4][0][1] = copy[1][1][2];
          this.rubikCube[4][0][2] = copy[1][2][2];

          this.rubikCube[3][0][0] = copy[4][0][2];
          this.rubikCube[3][1][0] = copy[4][0][1];
          this.rubikCube[3][2][0] = copy[4][0][0];
        }
      } else if (this.selected[3]) {
        if (direction === 1) {
          // yellow
          this.rubikCube[3][0][0] = copy[3][0][2];
          this.rubikCube[3][0][1] = copy[3][1][2];
          this.rubikCube[3][0][2] = copy[3][2][2];
          this.rubikCube[3][1][0] = copy[3][0][1];

          this.rubikCube[3][1][2] = copy[3][2][1];
          this.rubikCube[3][2][0] = copy[3][0][0];
          this.rubikCube[3][2][1] = copy[3][1][0];
          this.rubikCube[3][2][2] = copy[3][2][0];

          this.rubikCube[0][0][2] = copy[5][0][2];
          this.rubikCube[0][1][2] = copy[5][1][2];
          this.rubikCube[0][2][2] = copy[5][2][2];

          this.rubikCube[2][0][2] = copy[0][0][2];
          this.rubikCube[2][1][2] = copy[0][1][2];
          this.rubikCube[2][2][2] = copy[0][2][2];

          this.rubikCube[4][0][2] = copy[2][0][2];
          this.rubikCube[4][1][2] = copy[2][1][2];
          this.rubikCube[4][2][2] = copy[2][2][2];

          this.rubikCube[5][0][2] = copy[4][0][2];
          this.rubikCube[5][1][2] = copy[4][1][2];
          this.rubikCube[5][2][2] = copy[4][2][2];
        }
      } else if (this.selected[4]) {
        if (direction === 1) {
          // red
          this.rubikCube[4][0][0] = copy[4][0][2];
          this.rubikCube[4][0][1] = copy[4][1][2];
          this.rubikCube[4][0][2] = copy[4][2][2];
          this.rubikCube[4][1][0] = copy[4][0][1];

          this.rubikCube[4][1][2] = copy[4][2][1];
          this.rubikCube[4][2][0] = copy[4][0][0];
          this.rubikCube[4][2][1] = copy[4][1][0];
          this.rubikCube[4][2][2] = copy[4][2][0];

          this.rubikCube[1][2][0] = copy[2][2][0];
          this.rubikCube[1][2][1] = copy[2][2][1];
          this.rubikCube[1][2][2] = copy[2][2][2];

          this.rubikCube[2][2][0] = copy[3][2][0];
          this.rubikCube[2][2][1] = copy[3][2][1];
          this.rubikCube[2][2][2] = copy[3][2][2];

          this.rubikCube[3][2][0] = copy[5][0][2];
          this.rubikCube[3][2][1] = copy[5][0][1];
          this.rubikCube[3][2][2] = copy[5][0][0];

          this.rubikCube[5][0][2] = copy[1][2][0];
          this.rubikCube[5][0][1] = copy[1][2][1];
          this.rubikCube[5][0][0] = copy[1][2][2];
        }
      } else if (this.selected[5]) {
        if (direction === 1) {
          // red
          this.rubikCube[5][0][0] = copy[5][0][2];
          this.rubikCube[5][0][1] = copy[5][1][2];
          this.rubikCube[5][0][2] = copy[5][2][2];
          this.rubikCube[5][1][0] = copy[5][0][1];

          this.rubikCube[5][1][2] = copy[5][2][1];
          this.rubikCube[5][2][0] = copy[5][0][0];
          this.rubikCube[5][2][1] = copy[5][1][0];
          this.rubikCube[5][2][2] = copy[5][2][0];

          this.rubikCube[0][0][0] = copy[1][2][0];
          this.rubikCube[0][0][1] = copy[1][1][0];
          this.rubikCube[0][0][2] = copy[1][0][0];

          this.rubikCube[1][2][0] = copy[4][2][0];
          this.rubikCube[1][1][0] = copy[4][2][1];
          this.rubikCube[1][0][0] = copy[4][2][2];

          this.rubikCube[3][2][2] = copy[0][0][2];
          this.rubikCube[3][1][2] = copy[0][0][1];
          this.rubikCube[3][0][2] = copy[0][0][0];

          this.rubikCube[4][2][0] = copy[3][2][2];
          this.rubikCube[4][2][1] = copy[3][1][2];
          this.rubikCube[4][2][2] = copy[3][0][2];
        }
      }
      // update view
      this.rubikCube = Object.assign([], this.rubikCube);
    },
    select(i) {
      this.selected = [0, 0, 0, 0, 0, 0];
      this.selected[i] = 1;
    }
  }
};
</script>
<style>
.inline {
  display: inline-table;
}
</style>
