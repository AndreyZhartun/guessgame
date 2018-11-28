:- data_source(words,
               csv('https://raw.githubusercontent.com/qeetree/guessgame/master/words2.csv',
                   [])).

guesscycle(_, 0) :-!.
guesscycle(Num, Word, Tries) :-
    NewTries is Tries - 1,
    write('Введите слово или \'giveup\' для прекращения игры:'),
    read(Something),
    (   Something == giveup -> true;   
    	Something == Word ->  true;
    	write('Неверно, осталось попыток: '),
        writeln(NewTries),
        guesscycle(Num, Word, NewTries)
    ).    

guessgame :-
    write('Введите номер:'),
    read(Num),
    data_row(words, words(Num, Word, Desc)) ->  (
                                          write('Описание слова: '),
                                          writeln(Desc),
                                          guesscycle(Num, Word, 3)).
