<template>
  <ModalComponent
    :visibility="modalVisibility"
    :message="winnerMessage"
    @close="handleModalVisibility"
  />
  <GameBoard
    @startGame="handleStartGame"
    :marks="marks"
    :shadowVisibility="shadowVisibility"
  />
</template>

<script>
import GameBoard from "./components/GameBoard.component.vue";
import ModalComponent from "./components/ModalWinner.component.vue";

export default {
  components: {
    GameBoard,
    ModalComponent,
  },
  data() {
    return {
      modalVisibility: false,
      winnerMessage: "", // Add this variable to store the winner message
      currentPlayerChoice: "X", // Initial player choice
      marks: Array(9).fill(null), // Array for cell marks
      shadowVisibility: { X: true, O: false }, // Control shadow visibility for each player
    };
  },
  methods: {
    handleModalVisibility() {
      this.modalVisibility = !this.modalVisibility;
      if (!this.modalVisibility) {
        this.handleResetGame(); // Reset game when modal is closed
      }
    },
    handleStartGame(index) {
      if (!this.marks[index]) {
        this.marks[index] = this.currentPlayerChoice;
        this.shadowVisibility = { X: false, O: false }; // Toggle shadow visibility
        this.declareWinner(); // Check for a winner
        this.currentPlayerChoice = this.currentPlayerChoice === "X" ? "O" : "X"; // Switch players
        this.shadowVisibility[this.currentPlayerChoice] = true; // Update shadow for next player
      }
    },
    handleResetGame() {
      this.marks = Array(9).fill(null);
      this.currentPlayerChoice = "X";
      this.shadowVisibility = { X: true, O: false };
      this.winnerMessage = ""; // Reset winner message
    },
    declareWinner() {
      const winningCombinations = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];

      for (const combination of winningCombinations) {
        const [a, b, c] = combination;
        if (
          this.marks[a] &&
          this.marks[a] === this.marks[b] &&
          this.marks[a] === this.marks[c]
        ) {
          this.winnerMessage = `${this.marks[a]} GANHOU!`; // Set the winner message
          this.modalVisibility = true; // Show modal
          return; // Exit after declaring a winner
        }
      }
      if (this.marks.every((mark) => mark !== null)) {
        this.winnerMessage = "EMPATE!"; // Set the draw message
        this.modalVisibility = true; // Show modal
      }
    },
  },
  watch: {
    marks() {
      this.declareWinner(); // Check for a winner whenever marks change
    },
  },
};
</script>
