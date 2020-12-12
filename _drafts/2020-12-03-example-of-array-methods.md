---
title: "Learning Ruby: Examples of Array methods"
categories: programming
---


grades = [4, 6, 3, 2, 1, 5, 3, 4, 5, 2, 3, 5, 6, 4, 5]

puts 'Liczba ocen: ' + grades.size.to_s
puts 'Srednia: ' + (grades.sum.to_f / grades.size).to_s

puts "Pierwszy element tablicy: " + grades[0].to_s
puts "Drugi element tablicy: " + grades[1].to_s
puts "Trzeci element tablicy: " + grades[2].to_s

puts "Najwyzsza ocena: " + grades.max.to_s
puts "Najwyzsza ocena: " + grades.min.to_s

names = ["Kasia", "Patryk", "Ania", "Zorka"]

puts "Pozycja elementu w tablicy ocen: " + grades.index(2).to_s
puts "Pozycja elementu w tablicy imion: " + names.index("Zorka").to_s
puts "Pozycja elementu w tablicy imion: " + names.index("Kasia").to_s

numbers = [10, 5]
smaller = numbers.min
bigger = numbers.max
puts "Wiekszy jest: " + bigger.to_s
puts "Mniejszy jest: " + smaller.to_s
puts "Roznica to: " + (bigger - smaller).to_s

array = []

puts "Podaj mi liczby"

array.push(gets.chomp)
array.push(gets.chomp)
array.push(gets.chomp)
array.unshift(gets.chomp)
array.unshift(gets.chomp)

puts "Tablica to: " + array.inspect
puts "Ilosc elementow w tablicy: " + array.size.to_s

puts "Wyciagam pierwszy element z tablicy: " + array.shift.to_s
puts "Tablica to: " + array.inspect



 