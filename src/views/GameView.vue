<script setup lang="ts">
import Square from '@/components/Square.vue';
import { ref } from 'vue';

const squares = ref<Array<any>[8] | null>(Array(9).fill(null));
const isPlayerXTurn = ref(false);
const hasWinner = ref<null | string>(null)
const status = ref("Next player: O");

// Returns either 'X' or 'O' if the user wins
// Returns null if there's 
function calculateWinner(squares: any[8]) {
    const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
    ];
    for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
            return squares[a];
        }
    }
    return null;
}

// TODO: Potentially need to modify this so we only call getWinner once.
function handleClick(index: number) {
    const nextSquare = squares.value.slice();

    // Check if there's no current winner and square is not occupied by someone
    if ((hasWinner.value == null) && (squares.value[index] == null)) {
        if (isPlayerXTurn.value) {
            nextSquare[index] = 'X';
        } else {
            nextSquare[index] = 'O';
        }
        // Invert the player
        isPlayerXTurn.value = !isPlayerXTurn.value;
        squares.value = nextSquare;

        // Check if there's any winner
        hasWinner.value = calculateWinner(nextSquare);

        if (hasWinner.value) {
            status.value = `The Winner is ${hasWinner.value}`
        }
        else if (!isGameOver(nextSquare)) {
            status.value = `Next player: ${(isPlayerXTurn.value) ? 'X' : 'O'}`;
        }
        else {
            status.value = `Game has ended with no winners`;
        }
    }
}

function isGameOver(squares: any[8]) {
    let filteredArray = squares.filter((square: any) => square == null);
    if (filteredArray.length != 0) {
        return false;
    }
    return true;
}

// Return a 10 when AI wins 
// Return a -10 when player loses (Intended)
// Return 0 if game has not ended.
// TODO: Set this to be more flexible so that user can ask for "hint" instead of only being restricted to user.
function score(board: Array<any>[8]): number {
    let winner = calculateWinner(board);
    if (winner == 'X') {
        return 10;
    } else if (winner == 'O') {
        return -10;
    }
    return 0;
}

function minimax(board: Array<any>[8]) {

}

</script>

<template>
    <div class=" h-screen flex flex-col mx-auto container items-center justify-center">
        <div class="text-2xl font-light">{{ status }}</div>
        <div class="pt-4">
            <div class="flex">
                <Square :value="squares[0]" @click="handleClick(0)" />
                <Square :value="squares[1]" @click="handleClick(1)" />
                <Square :value="squares[2]" @click="handleClick(2)" />
            </div>
            <div class="flex">
                <Square :value="squares[3]" @click="handleClick(3)" />
                <Square :value="squares[4]" @click="handleClick(4)" />
                <Square :value="squares[5]" @click="handleClick(5)" />
            </div>
            <div class="flex">
                <Square :value="squares[6]" @click="handleClick(6)" />
                <Square :value="squares[7]" @click="handleClick(7)" />
                <Square :value="squares[8]" @click="handleClick(8)" />
            </div>
        </div>
    </div>
</template>