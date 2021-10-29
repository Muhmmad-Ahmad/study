import java.lang.NumberFormatException
import java.util.Locale
import kotlin.system.exitProcess

fun main() {
    menuHold()
}

/** Amount of rows */
fun readNextInt1(): Int {
    println("Enter the number of rows:")
    return try {
        val aIn = readLine()!!.toInt()
        if (aIn <= 0) {
            throw NumberFormatException()
        } else {
            aIn
        }
    } catch (e: NumberFormatException) {
        println("Wrong input!")
        readNextInt1()
    }
}

/** Amount of seats */
fun readNextInt2(): Int {
    println("Enter the number of seats in each row:")
    return try {
        val bIn = readLine()!!.toInt()
        if (bIn <= 0) {
            throw NumberFormatException()
        } else {
            bIn
        }
    } catch (e: NumberFormatException) {
        println("Wrong input!")
        readNextInt2()
    }
}

val a = readNextInt1() // Rows of cinema room
val b = readNextInt2() // Seats of cinema room
val totalSeats = a * b // Total
var purchasedTickets = 0
var currentIncome = 0
var placementPercentage: Double = 0.0

/** Table of cinema */
val cinema = MutableList(a) {
    MutableList(b) {'S'}
}

/** Print cinema */
fun cinemaRoom() {
    // Indexes "X"
    var baseIndexX = emptyArray<Int>()
    for (i in 1..b) {
        baseIndexX += i
    }
    println("Cinema:")
    println("  ${baseIndexX.joinToString().replace(",","")}")

    // Indexes "Y"
    for (i in 0 until cinema.size) {
        println("${i + 1} ${cinema[i].joinToString().replace(",","")}")
    }
    menuHold()
}

/**  Function seat bought */
fun cinemaPlaceBought(cinema: MutableList<MutableList<Char>>, checkRow: Int, checkSeat: Int) {
    /**  Changing place in cinema room */
    try {
        if (cinema[checkRow - 1][checkSeat - 1] == 'S') {
            cinema[checkRow - 1][checkSeat - 1] = 'B'
            purchasedTickets++
            placementPercentage = (purchasedTickets.toDouble() / totalSeats) * 100
            currentIncome += priceChecker(checkRow, checkSeat)
            println("Ticket price: $${priceChecker(checkRow, checkSeat)}")
        } else if (cinema[checkRow - 1][checkSeat - 1] == 'B') {
            println("That ticket has already been purchased!")
            buyTicket()

            /***  Checking Room fullness ***/
        } else if (cinema[cinema.size][cinema.size] != 'S') {
            println("Sorry, cinema room doesn't have any space")
            menuHold()
        }
    } catch (e: Exception) {
        println("Error again")
    }
}

/**  Input for seat and row for buying ticket */
fun buyTicket() {
    println("")
    /**  Row and Seats parameters */
    var checkRow = 0
    var checkSeat = 0
    try {
        /**  Input Row */
        println("Enter a row number:")
        val rowIn = readLine()!!.toInt()
        if (rowIn <= 0 || rowIn > a) {
            throw NumberFormatException()
        } else {
            checkRow = rowIn
        }
        /**  Input Seats */
        println("Enter a seat number in that row:")
        val seatIn = readLine()!!.toInt()
        if (seatIn <= 0 || seatIn > b) {
            throw NumberFormatException()
        } else {
            checkSeat = seatIn
        }
    } catch (e: NumberFormatException) {
        println("Wrong input!")
        buyTicket()
    } catch (e: Exception) {
        println("Wrong input!")
        buyTicket()
    }

    /**  Process of changing seat from 'S' to 'B' */
    if (checkRow != 0 && checkSeat != 0) {
        cinemaPlaceBought(cinema, checkRow, checkSeat)
        menuHold()
    } else { return }
}

/**  Price checker */
fun priceChecker(checkRow: Int, checkSeat: Int): Int {
    return when {
        totalSeats <= 60 -> { 10 }
        checkRow in 0..a - 5 -> { 10 }
        else -> { 8 }
    }
}

fun totalIncomeChecker(): Int {
    return when {
        totalSeats <= 60 -> { totalSeats * 10 }
        else -> {
            ((totalSeats - (a - 5) * b) * 8) + ((a - 5) * b) * 10
        }
    }
}

/**  Statistic menu show */
fun statistics() {
    println("Number of purchased tickets: $purchasedTickets")
    println("Percentage: ${"%.2f".format(Locale.US, placementPercentage) + "%"}")
    println("Current income: $${currentIncome}")
    println("Total income: $${totalIncomeChecker()}")
    menuHold()
}

/**  Menu of Program */
fun menuHold() {
    println("")
    println("1. Show the seats")
    println("2. Buy a ticket")
    println("3. Statistics")
    println("0. Exit")
    when (readLine()!!.toInt()) {
        1 -> cinemaRoom()
        2 -> buyTicket()
        3 -> statistics()
        0 -> return // Exit program
        else -> {
            println("Unknown command, please try again")
            menuHold()
        }
    }
}
