Брифинг: Тестирование мода Exotica Tech.
С Shark у меня языковой барьер и ввиду этого барьера возникли трудности.

Задача такая - нужно протестировать мод с документацией всех действий и возникших проблем при тестировании будь это баг или неисправность.

Человек не любит анализировать данные(Raw Data) и применяет ИИ для анализа. Поэтому ему нужно предоставить материал с конкретикой.
Я конечно не чертов научный сотрудник от чего хотят от меня подобной подачи, но попробую. Времени осталось мало, скоро ехать за город.

Переводы с английского:

Четверг, 22 октября 2026-ой год.

Сообщение -

Перевод:

В качестве вступления:

как только вы запустите эту новую игру (тестируйте на новых сохранениях, не тестируйте это дерьмо на уже существующей игре) — перед тем как сесть на планету (но после ввода необходимых консольных команд), полностью очистите свой starsector.log.
Откройте новый файл в Блокноте. 

Напишите там что-то вроде:

```
text
// делаю X (например, устанавливаю SpooledFeeders)
```

Затем зайдите в меню оснащения (refit), сделайте это действие и скопируйте логи из starsector.log в этот файл Блокнота.
Если возможно, оставляйте подсказки (комментарии) над определенными блоками логов. 
Но это не строго обязательно.
Что действительно (по возможности) необходимо — так это свести к минимуму количество логов, которые вы в итоге упустите 🙂 

Размер starsector.log ограничен 50 МБ.
Если проводить слишком много времени в меню оснащения с включенной диагностикой, он забьется очень быстро. Чтобы не потерять данные, перейдите, например, во вкладку груза (cargo) — это остановит непрерывную выдачу логов(правда, это может в некоторой степени исказить результаты теста, если изменятся идентификаторы вариантов оснащения), но об этом мы побеспокоимся позже.
Так что давайте проведем расследование и посмотрим, что там можно раскопать


  Пятница, 23 октября 2026-ой год.
  
Сообщение -
Перевод:

содержит дохренища логов и тест fullmetalsalvo
ExoticaTechnologies-diag.rar

Тест alphasubcore вам не нужен, я знаю, что передача эффектов там работает нормально. В основном он использовался для создания, проверки и валидации доступности между дочерними элементами (child-to-child reachability) и всякого прочего.

Так что если в каких-то тест-планах упоминается тест alphasubcore, а затем говорится о баффах характеристик... просто игнорируйте эту небольшую часть, тест alphasubcore делал то же самое, что и тест fullmetalsalvo.

Постарайтесь организовать логи так, чтобы в них был смысл.
Один лог-файл на один тест-план. Прекращать выполнение тест-планов после того, как они «упали» (fail), — это нормально, но вы ДОЛЖНЫ дать мне контекст.

Например: «после выполнения шагов 1–5 тест упал на шаге 6 с <детали дефекта>».
Чем больше логов вы соберете, тем лучше. Избегайте дублирования логов. Сто или сотни мегабайт — это всё ещё приемлемо.
(Но уберите из них весь шум. Направляйте в канал #shark-tank)
Раньше я часто делал так в этих массивах логов: оставлял дамп логов, а после него писал:
```
text
//VERDICT - FAIL: after ship1 installed AlphaSubcore on right child, ship1's right child and root module have decreased OP but left child was left unaffected

(//ВЕРДИКТ — ПРОВАЛ: после того как ship1 установил AlphaSubcore на правый дочерний элемент, у правого дочернего элемента и корневого модуля ship1 снизился OP, но левый дочерний элемент остался незатронутым)
```
Чтобы, если вы прогоняете один тест-план, вы могли выцепить парочку таких ВЕРДИКТОВ после упавших шагов, объясняющих, что именно пошло не так. Логи расскажут остальную часть истории (на самом деле они расскажут всю историю целиком, но эти «вердикты» дают точку опоры и контекст).



English..

Четверг, 22 октября 2026-ой год.
Сообщение -
Shark.
as a prelude, once you start this new game (test on new games, don't test this shit on an existing game) - before you enter the planet (but after you entered necessary console commands), clean out your starsector.log

open up a new notepad file. put something like
```
// doing X (e.g. installing SpooledFeeders)
```
then go to refit, do the action, copy the logs from starsector.log into the notepad file. if possible, put a hint above some block of logs. this isn't strictly necessary though.

what is somewhat necessary (to try) is to minimize the amount of logs you'll end up missing 🙂 starsector.log is capped at 50mb. 
spending too much time in refit with diagnostics will fill that up quick. to avoid losing it, go to e.g. cargo, that will stop pumping out logs
(but might also _somewwhat_ invalidate testing if refit variants identity changes) but, we'll worry about that later.

so lets investigate and see whats there to see.


---------------------------------------------------------------------------------------------------------------------------------

Пятница, 23 октября 2026-ой год.
Сообщение -
Shark:
has a shitload of logs in it, and the test fullmetalsalvo
ExoticaTechnologies-diag.rar

you don't need the test alphasubcore, i know the effect sharing works fine there, and it's mostly been to make/check/validate child-to-child reachability and other shit. 
so if some plans mention test alphasubcore and then mention stats buffs... just ignore that little part, the test alphasubcore did the same this test fullmetalsalvo did.
try to organize logs so that they make sense.
one log file per plan. bailing out on plans after it 'fails' is fine, but you are going to HAVE TO give me context, e.g. "after doing steps 1-5, it failed on step6 with <details on defect>"
the more logs you collect, the better. avoid duplicated logs. hundred or hundreds of megabytes is still acceptable. 
(but remove all noise from them.⁠shark-tank⁠)

one thing i used to do in these log blobs is leaving a log dump followed by
```
//VERDICT - FAIL: after ship1 installed AlphaSubcore on right child, ship1's right child and root module have decreased OP but left child was left unnaffected
```

Суббота, 24 октября.
Shark:
just so we're on the same page here - i will most likely not spend 30-90 minutes bleeding my eyes out sifting through these logs.
i will pass them onto AI and say "here's what happened, <this> should have happened but instead <something else> happened. trace down the logic faults/gaps that led to this problem so we can come up with a way to fix it".

the logs are <proof> of what happened. the code is the scaffold of <what should> be happening. i have a pretty good idea of the "product" and it's desired behaviour. the difference between the <proof>, <what should> and <what should really be happening / what was expected to happen> is the thing that leads to proper surgical bugfixes.
so i will also need to give it context so it can use this shit load of text and figure out where the problem happened and why that's a problem (because something else should have happened).

example: simple case is "after installing exotic1 on child1, and exotic2 on child2 we should end up with [exotic1, exotic2] exoticas on the whole ship, installed on child1 and child2 respectively. instead - after installing exotic2 on child2, we ended up with exotic2 on child1 and exotic1 on child2. or something else. trace down why it's happening".


Because, while the shit i did in 2.1.0 was "great", i also "accidentally" left a very subtle super-hard-to-trace-down bug in there that ended up killing exoticas on child modules. the problem wasn't with the "idea" part of it, there was a small brainfart problem in the implementation which was overlooked due to eventually shifting test focus completely to HullmodExotics, believing that what used to work until then will keep on working and doesn't have to be re-tested constantly. that's where i was wrong.

so yea, i had two options. 1) bleed my eyes out and find the small problem <somewhere>, or 2) create a harness to bring in some help to help me better pinpoint the problem.

so after doing 2) in less time than it'd take me to do 1) and giving it 170mb of various logs, it pointed out exactly 6 lines which were causing it to behave that way. and indeed, i said "well this isn't right, omg" and fix it within ~30mins. 

tl;dr AI isn't quite 'great' at producing high-quality fancy-looking code. but it is great at consuming huge amounts of text and pinpointing where exactly (and why) the difference between "what actually happened" and "what should have happened" really happened.
so that if you run through one test plan, you might pick up a few of these VERDICTS after failing steps, explaining what went wrong. the logs will tell the rest of the story (they'll actually tell the whole story but these 'verdicts' provide grounding and context)

this is what we're doing now.
providing context in the logs themselves is nice. not entirely necessary but it helps. but providing step-by-step context out of logs is a must. 
- i installed <this> <here>
- PASS: after checking, <this> was indeed on <here>
- i installed <that> <there>
- FAIL: instead of having <this> on <here> and <that> on <there> I ended up with <actual result>

this is just a bullshit example. i will not insist on being so verbose but it certainly helps. gates that say PASS/FAIL in the logs help, but aren't super necessary as the outcome of the whole test run is enough, with the information on which step it failed. but the test plan must include verification/validation steps 🙂
so then when we figure out which part of the mod is the source of the problem, we just fix that little thing. and add that test plan (the one that was failing) to the set of test plans which are always expected to pass - and have to be used as QA gates after touching any of the mod's under-the-hood internals. (this is the step i was missing that led to 2.1.0 being released as-is)

блаблаблабла(21:36, 25 october)
------------------------------------------------------------------------------------------------------------------------------
