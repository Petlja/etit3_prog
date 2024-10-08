# Добре и лоше праксе коришћења изузетака

Током изучавања претходних лекција, вероватно си добио идеју да помоћу
изузетака можеш да контролишеш ток извршавања програма. На пример, ако је бачен
изузетак уради нешто, а у супротном уради нешто друго.
**Никада немој да користиш изузетке као механизам за контролу тока програма!**
Изузетке користи искључиво за обраду грешака које се јављају током извршавања
програма. Користи их мудро, онда када су неопходни - у изузетним ситуацијама.

**Труди се да могуће грешке прецизираш.** Хватање сувише општих изузетака, нпр.
`Exception` изузетака, може сакрити проблеме и отежати отклањање грешака. Добра
пракса налаже да идентификујеш специфичне изузетке који могу да се баце, ухвате
и обраде појединачно.

**Немој да игноришеш изузетке.** Хватање изузетка и не предузимање никакве
акције поводом тога може да доведе до неочекиваних понашања програма. Укратко,
никада не остављај поље `catch` празно!

**Немој да бацаш изузетке прекомерно.** Изузеци су "скупа" операција, па
прекомерно бацање изузетака може да доведе до лоших перформанси. Увек покушај
да решиш потенцијалне проблеме и на неки други начин, најпре писањем класа у
којима је смањена могућност појаве изузетака.

**Немој да бацаш изузетке уместо да враћаш резултате.** Изузеци нису замена за
регуларне повратне вредности. Такође, изузетке не треба да користиш као
повратне вредности или параметре, када треба да буду бачени.

**Изузеци се не смеју појављивати било где у програму.** Кôд у блоку `finally`
не сме да баци изузетак. Такође, неке методе попут `Equals`, `GetHashCode` и
`ToString` не смеју да бацају изузетке. На крају, ни статички конструктори и
оператори једнакости не смеју да бацају изузетке.

**Води рачуна о ресурсима и меморији.** Када радиш са ресурсима као што су
фајлови, мрежне везе или базе података, увери се да су они правилно затворени у
`finally` блоку. У пракси се `finally` блок управо и користи за ослобађање
ресурса или извршавање кода који мора бити извршен без обзира на то да ли је
изузетак бачен или не.

**Користи логовање изузетака.** Поред исписа грешке у конзоли или у прозору за
поруке, добра пракса је да грешку забележиш и у одређеном `.log` фајлу. Постоје
готова решења за .NET попут log4net, NLog и Serilog, које можеш да користиш за
логовање изузетака. Можеш накнадно да прочиташ`.log` фајл, па не мораш да се
ослањаш на информације о грешци које ти је дао корисник апликације.
