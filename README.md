import { useState } from "react";

const CONTENT_TYPES = {
  REEL: { label: "Reel 🎬", color: "#f43f5e", bg: "#f43f5e18" },
  MEME: { label: "Meme 😭", color: "#a855f7", bg: "#a855f718" },
  ENGAGE: { label: "Engage 💬", color: "#06b6d4", bg: "#06b6d418" },
  STORY: { label: "Story ✨", color: "#f59e0b", bg: "#f59e0b18" },
  PROMO: { label: "Promo 🔥", color: "#10b981", bg: "#10b98118" },
  UGC: { label: "UGC 🤳", color: "#ec4899", bg: "#ec489918" },
};

const days = [
  {
    day: 1,
    type: "REEL",
    title: "The Origin Story POV",
    caption: `POV: you're about to eat something that will ruin all other snacks for you forever 💀🐙\n\n#TakoCrave #Takoyaki #FoodPH #GenZEats #YouWereWarned`,
    hook: "POV hook — most viral Gen Z format",
    visual: "Slow zoom into golden takoyaki balls sizzling on the pan. Add trending audio.",
    cta: "Tag someone who needs to try this ASAP",
  },
  {
    day: 2,
    type: "MEME",
    title: "Broke But Craving Meme",
    caption: `Me: I'm saving money this month 💪\nTako Crave notification: 👁👄👁\n\nbestie said it's only ₱XX for 6 pcs. my savings said goodbye 💸\n\n#TakoCrave #Relatable #BrokeSzn #TakoyakiPH`,
    hook: "Self-aware broke humor = Gen Z goldmine",
    visual: "Two-panel meme format. Left: serious face. Right: already ordering.",
    cta: "Like this if your wallet is also suffering",
  },
  {
    day: 3,
    type: "ENGAGE",
    title: "This or That: Sauce Edition",
    caption: `real ones know which one hits different 👇\n\nSpicy mayo 🌶️ OR Japanese mayo 🍶\n\ncomment your answer and don't be shy bestie\n\n#TakoCrave #ThisOrThat #Takoyaki #FoodDebate`,
    hook: "Easy engagement — forces a choice, everyone has an opinion",
    visual: "Split graphic: both sauces side by side, aesthetic flat lay.",
    cta: "Comment below — no wrong answers (jk there are)",
  },
  {
    day: 4,
    type: "REEL",
    title: "ASMR Sizzle Reel",
    caption: `no talking. just vibes. 🐙🔥\n\nthis sound lives in my head rent free\n\n#TakoCrave #ASMR #FoodASMR #TakoyakiASMR #SatisfyingFood`,
    hook: "ASMR content = massive retention + shares",
    visual: "Close-up sizzle sounds. Batter poured. Flip. Sauce drizzle. No music, just sound.",
    cta: "Save this for when you need to calm down lol",
  },
  {
    day: 5,
    type: "MEME",
    title: "Loyalty Test Meme",
    caption: `if you haven't tried Tako Crave yet we can't be friends. i don't make the rules. 🤷‍♀️\n\n#TakoCrave #JustSaying #Takoyaki #FoodiesOfIG #ManillaEats`,
    hook: "Exclusivity humor — Gen Z loves fake gatekeeping",
    visual: "Clean bold text over aesthetic background. Minimal. Punchy.",
    cta: "Tag your friend who still hasn't tried it 👇",
  },
  {
    day: 6,
    type: "STORY",
    title: "Behind the Scenes: Morning Prep",
    caption: `6AM and we're already out here making your snack obsession possible 😤\n\nthe dedication is unmatched fr fr\n\n#BehindTheScenes #TakoCrave #SmallBusiness #HardWork`,
    hook: "Authenticity and hustle = Gen Z respects it",
    visual: "Raw, unfiltered morning prep. Ingredients laid out. Batter mixing. Real life.",
    cta: "Drop a 🐙 if you appreciate the grind",
  },
  {
    day: 7,
    type: "ENGAGE",
    title: "Rate Your Order 1-10",
    caption: `rate your Tako Crave experience bestie 👇\n\n1-3: okay ka lang\n4-6: it was fine ig\n7-9: sending this to everyone i know\n10: my personality is takoyaki now\n\n#TakoCrave #RateIt #Takoyaki #FoodReview`,
    hook: "Rating systems get wild comment threads",
    visual: "Aesthetic rating graphic with takoyaki art. Playful font.",
    cta: "We're manifesting all 10s in the comments",
  },
  {
    day: 8,
    type: "REEL",
    title: "First Bite Reaction Compilation",
    caption: `the face you make after your first Tako Crave bite is a whole personality 😭💀\n\nwe see you. we love you.\n\n#TakoCrave #FirstBite #CustomerReaction #Takoyaki #FoodTok`,
    hook: "Real reactions = most authentic social proof",
    visual: "Compilation of real customer first-bite faces. Funny cuts. Fast paced.",
    cta: "Send this to someone who needs to experience this",
  },
  {
    day: 9,
    type: "MEME",
    title: "3AM Craving Meme",
    caption: `3am brain: sleep\nalso 3am brain: tako crave 🐙\n\ni am NOT well and that's their fault\n\n#TakoCrave #3amCravings #Relatable #Takoyaki #SendHelp`,
    hook: "3AM content = peak relatable Gen Z humor",
    visual: "Dark aesthetic meme. Moon emoji. Dramatic font.",
    cta: "Tell me I'm not the only one 😭",
  },
  {
    day: 10,
    type: "PROMO",
    title: "Bundle Drop Announcement",
    caption: `NEW BUNDLE just dropped and your wallet is NOT ready 🔥\n\n6 pcs + 12 pcs options now available\nmore takoyaki = more happiness. the math is MATHING.\n\nLink in bio or DM us bestie 💌\n\n#TakoCrave #NewDrop #TakoyakiBundle #LimitedOffer`,
    hook: "Hype drop language = Gen Z buying behavior trigger",
    visual: "Product flat lay. Clean. Bold price. Limited time badge.",
    cta: "DM us NOW before it's gone 🏃‍♀️",
  },
  {
    day: 11,
    type: "REEL",
    title: "Day in the Life of Tako Crave",
    caption: `day in my life as a takoyaki small biz owner 🐙✨\n\nspoiler: it's chaotic and i love it\n\n#SmallBusiness #DayInMyLife #TakoCrave #BehindTheBusiness #EntrepreneurLife`,
    hook: "Day-in-the-life = highest watch time format",
    visual: "Vlog-style. Alarm. Prep. Customers. Closing. Honest and fun.",
    cta: "Would you want to run a food biz? Comment 👇",
  },
  {
    day: 12,
    type: "MEME",
    title: "Friend Group Roles Meme",
    caption: `every friend group has one:\n\n🐙 the one who discovered Tako Crave first\n😤 the one who said "sus yan" but ate 12 pcs\n💸 the one who always forgets their wallet\n😭 the one who cries when it sells out\n\nwhich one are you? 👇\n\n#TakoCrave #FriendGroup #Relatable #Takoyaki`,
    hook: "Friend group assignment = mass tagging behavior",
    visual: "List format meme. Clean icons. Viral carousel potential.",
    cta: "Tag your group and assign roles 😭",
  },
  {
    day: 13,
    type: "STORY",
    title: "Poll: Spicy or OG Flavor?",
    caption: `we need answers and we need them NOW 👇\n\nSpicy Tako 🌶️ vs Classic Tako 🐙\n\nvote on our story! your answer might decide our next flavor drop 👀\n\n#TakoCrave #Poll #NewFlavor #YouDecide`,
    hook: "Polls that affect real decisions = high participation",
    visual: "Story poll sticker. Dramatic 'YOU DECIDE' text overlay.",
    cta: "Vote on our story right now!",
  },
  {
    day: 14,
    type: "UGC",
    title: "Customer Feature Friday",
    caption: `not us crying because y'all are too cute 😭🐙\n\nshoutout to @[customer] for this 10/10 content\n\nwant to be featured? tag us or use #TakoCrave when you post!\n\n#CustomerLove #TakoCrave #Repost #FoodCommunity`,
    hook: "UGC = free content + community building + trust",
    visual: "Repost customer photo with branded frame. Tag them prominently.",
    cta: "Post your Tako Crave moment and we just might feature you 👀",
  },
  {
    day: 15,
    type: "REEL",
    title: "Satisfying Takoyaki Flip Reel",
    caption: `the flip that lives in my head 24/7 🐙✨\n\nsomeone said this is better than therapy and honestly same\n\n#TakoCrave #SatisfyingFood #TakoyakiFlip #FoodReels #Satisfying`,
    hook: "Satisfying content = highest share rate on Reels",
    visual: "Extreme close-up of the takoyaki flip. Perfect golden color. Slow mo.",
    cta: "Save this for your comfort content folder 🫶",
  },
  {
    day: 16,
    type: "ENGAGE",
    title: "Build Your Order",
    caption: `design your PERFECT Tako Crave order 👇\n\nPcs: 6 / 12 / 24\nSauce: spicy mayo / japanese mayo / both (correct answer)\nAdd-on: extra bonito / extra sauce / just give me more\n\ncomment your combo bestie!\n\n#TakoCrave #BuildYourOrder #Takoyaki #FoodCustom`,
    hook: "Build-your-own = high comment volume guaranteed",
    visual: "Clean menu-style graphic. Aesthetic and easy to read.",
    cta: "Your combo = your personality type actually",
  },
  {
    day: 17,
    type: "MEME",
    title: "Expectation vs Reality (But Reversed)",
    caption: `expectation: i'll just have a few pieces\nreality: 😭😭😭\n\n(the reality was 24 pieces and no regrets)\n\n#TakoCrave #ExpectationVsReality #Takoyaki #Relatable #NoRegrets`,
    hook: "Reversed expectations = Gen Z loves the subverted format",
    visual: "Two panel. Expectation looks boring. Reality = full table of takoyaki.",
    cta: "Tell me your Tako Crave intake record 👇",
  },
  {
    day: 18,
    type: "REEL",
    title: "Cheese Pull Close-Up",
    caption: `this is your sign to stop whatever you're doing 🧀🐙\n\nwe put CHEESE in it and you're still sleeping??\n\n#TakoCrave #CheesePull #TakoyakiCheese #FoodPorn #Satisfying`,
    hook: "Cheese pull = most shared food content format ever",
    visual: "Dramatic slow cheese pull. Warm lighting. No talking. Just the pull.",
    cta: "Tag someone who needs this in their life RIGHT NOW",
  },
  {
    day: 19,
    type: "STORY",
    title: "Q&A: Ask Tako Crave Anything",
    caption: `drop your questions bestie 👇\n\nflavor secrets? origin story? why is it so addicting?\nask us anything and we'll answer on our story 👀\n\n#TakoCrave #QandA #AskMeAnything #Takoyaki #SmallBiz`,
    hook: "Q&A = humanizes the brand + engagement spike",
    visual: "Question box sticker on story. Playful background.",
    cta: "Your most unhinged questions welcome 😭",
  },
  {
    day: 20,
    type: "PROMO",
    title: "Flash Sale — Today Only",
    caption: `🚨 FLASH SALE ALERT 🚨\n\nbecause it's [day] and you deserve a treat\n\nspecial price TODAY ONLY — check our story for details 👀\n\nfirst come first served bestie, don't say we didn't warn you 🏃\n\n#TakoCrave #FlashSale #TodayOnly #LimitedOffer #Takoyaki`,
    hook: "Urgency + scarcity = fastest conversion trigger",
    visual: "Bold red/orange announcement graphic. Timer aesthetic. FOMO energy.",
    cta: "DM us NOW or forever hold your craving 😤",
  },
  {
    day: 21,
    type: "REEL",
    title: "Trending Audio + Takoyaki Montage",
    caption: `when the takoyaki hits different at [time] on a [day] ✨🐙\n\n#TakoCrave #Takoyaki #FoodTok #TrendingAudio #JapaneseFood`,
    hook: "Riding trending audio = fastest discovery tool on Reels",
    visual: "Fast-cut aesthetic food montage synced to trending audio. Vibe-heavy.",
    cta: "Save + share if this is your current personality",
  },
  {
    day: 22,
    type: "MEME",
    title: "Apology Text But Make It Tako",
    caption: `me to my diet: i'm so sorry, i love you, but Tako Crave posted and i blacked out 😭\n\nit's not my fault it's literally irresistible\n\n#TakoCrave #DietWho #Relatable #Takoyaki #SorryNotSorry`,
    hook: "Apology text format = extremely viral Gen Z meme style",
    visual: "iPhone message bubble aesthetic. Dramatic apology text.",
    cta: "Repost if your diet has also been personally victimized",
  },
  {
    day: 23,
    type: "UGC",
    title: "Repost: Funniest Customer Caption",
    caption: `y'all are funnier than us and we're not even mad about it 😭\n\nshoutout to @[customer] for this caption we could NEVER\n\ntag us in your posts! best one gets featured 👀\n\n#TakoCrave #CustomerFeature #UGC #Takoyaki #Community`,
    hook: "Reposting funny customer content = viral loop starts",
    visual: "Screenshot of customer post with branded overlay. Keep it authentic.",
    cta: "Submit your best Tako Crave content 🎯",
  },
  {
    day: 24,
    type: "ENGAGE",
    title: "Unpopular Opinion Thread",
    caption: `unpopular opinion: takoyaki is better than pizza\n\ni said what i said 🐙\n\ndrop YOUR unpopular food opinion below — no judgment zone (there will be judgment)\n\n#TakoCrave #UnpopularOpinion #FoodDebate #Takoyaki`,
    hook: "Unpopular opinion = comment war = massive engagement",
    visual: "Bold statement card. Minimalist. Confident energy.",
    cta: "Agree or disagree? The comment section is open 👇",
  },
  {
    day: 25,
    type: "REEL",
    title: "The Takoyaki Making Process Start to Finish",
    caption: `from batter to your hands in [X] minutes 🐙✨\n\npov: you're watching your future snack be born\n\n#TakoCrave #HowItsMade #Takoyaki #ProcessVideo #FoodMaking`,
    hook: "Process videos = educational + satisfying + high save rate",
    visual: "Full process: mixing batter, pouring, flipping, plating, serving. Aesthetic angles.",
    cta: "Save this so you can watch it again when you're hungry 😭",
  },
  {
    day: 26,
    type: "MEME",
    title: "When Someone Says They Don't Like Takoyaki",
    caption: `when someone says they don't like takoyaki:\n\n👁👄👁\n\n...they just haven't had Tako Crave yet. that's the only explanation.\n\n#TakoCrave #Unacceptable #Takoyaki #Relatable #FixIt`,
    hook: "Defensive brand humor = loyalty signal to existing fans",
    visual: "Shocked meme face. Dramatic text. High contrast.",
    cta: "Bring them to us. We'll fix them. 🐙",
  },
  {
    day: 27,
    type: "STORY",
    title: "This Week's Best Customer Moment",
    caption: `our favorite customer moment this week goes to... 👀\n\n(check our story for the full clip/screenshot)\n\nthis community is unmatched fr 🫶\n\n#TakoCrave #CustomerLove #Community #WeeklyWrap`,
    hook: "Weekly wrap = builds habitual story checking",
    visual: "Story highlight with customer moment. Warm color grade.",
    cta: "Be our next featured moment — tag us 🐙",
  },
  {
    day: 28,
    type: "REEL",
    title: "Side-by-Side Flavor Comparison",
    caption: `classic vs spicy tako: a visual investigation 🔬🐙\n\nwe let the food speak for itself\n\n#TakoCrave #FlavorComparison #Takoyaki #WhichOne #FoodTest`,
    hook: "Comparison content = debate bait = comments flood in",
    visual: "Split screen. Both flavors plated beautifully. Same lighting. Let viewers choose.",
    cta: "Your answer in the comments decides our next promo 👀",
  },
  {
    day: 29,
    type: "PROMO",
    title: "End of Month Special + Teaser",
    caption: `month almost over and you still haven't tried Tako Crave??\n\nbabe. BABE. 😭\n\nspecial end-of-month treat waiting for you + something BIG coming next month 👀\n\n#TakoCrave #EndOfMonth #ComingSoon #Takoyaki #NewDrop`,
    hook: "Urgency + mystery teaser = follow for next month",
    visual: "Countdown aesthetic. Teaser blur on something new. FOMO design.",
    cta: "Follow so you don't miss next month's drop 🐙",
  },
  {
    day: 30,
    type: "ENGAGE",
    title: "30-Day Wrap + Community Love",
    caption: `30 days of Tako Crave and we're not stopping 🐙🔥\n\nthank you to everyone who ordered, shared, commented, and became part of this chaotic little community\n\nyou're the reason this hits different ✨\n\ncomment your fave Tako Crave moment this month 👇\n\n#TakoCrave #30Days #ThankYou #Community #Takoyaki`,
    hook: "Milestone + gratitude = emotional connection + reshares",
    visual: "Recap collage of the month. Customer photos. Moments. Warm energy.",
    cta: "Tell us your fave moment — we're reading every comment 🫶",
  },
];

const weekLabels = ["Week 1", "Week 2", "Week 3", "Week 4", "Week 5"];

export default function TakoCalendar() {
  const [selected, setSelected] = useState(null);
  const [filter, setFilter] = useState("ALL");
  const [copied, setCopied] = useState(false);

  const filtered = filter === "ALL" ? days : days.filter(d => d.type === filter);

  const handleCopy = (text) => {
    navigator.clipboard.writeText(text).then(() => {
      setCopied(true);
      setTimeout(() => setCopied(false), 2000);
    });
  };

  const getWeek = (dayNum) => Math.ceil(dayNum / 7);

  return (
    <div style={{
      fontFamily: "'Inter', -apple-system, sans-serif",
      background: "#080810",
      minHeight: "100vh",
      color: "#e2e8f0",
    }}>
      {/* Header */}
      <div style={{
        background: "linear-gradient(135deg, #0f0a1a 0%, #1a0a2e 100%)",
        padding: "24px 20px 20px",
        borderBottom: "1px solid #ffffff0f",
        textAlign: "center",
      }}>
        <div style={{ fontSize: 32, marginBottom: 6 }}>🐙</div>
        <h1 style={{
          fontSize: 22,
          fontWeight: 900,
          margin: 0,
          background: "linear-gradient(90deg, #f43f5e, #a855f7, #06b6d4)",
          WebkitBackgroundClip: "text",
          WebkitTextFillColor: "transparent",
          letterSpacing: -0.5,
        }}>
          Tako Crave
        </h1>
        <p style={{ fontSize: 12, color: "#94a3b8", margin: "4px 0 0", letterSpacing: 2, textTransform: "uppercase" }}>
          30-Day Gen Z Content Calendar
        </p>
      </div>

      {/* Filter Bar */}
      <div style={{
        display: "flex",
        gap: 8,
        padding: "14px 16px",
        overflowX: "auto",
        background: "#0d0b18",
        borderBottom: "1px solid #ffffff0a",
      }}>
        <button
          onClick={() => setFilter("ALL")}
          style={{
            padding: "6px 14px",
            borderRadius: 20,
            border: "1px solid",
            borderColor: filter === "ALL" ? "#a855f7" : "#ffffff15",
            background: filter === "ALL" ? "#a855f720" : "transparent",
            color: filter === "ALL" ? "#a855f7" : "#64748b",
            fontSize: 11,
            fontWeight: 700,
            cursor: "pointer",
            whiteSpace: "nowrap",
            letterSpacing: 0.5,
          }}
        >
          ALL 30
        </button>
        {Object.entries(CONTENT_TYPES).map(([key, val]) => (
          <button
            key={key}
            onClick={() => setFilter(key)}
            style={{
              padding: "6px 14px",
              borderRadius: 20,
              border: "1px solid",
              borderColor: filter === key ? val.color : "#ffffff15",
              background: filter === key ? val.bg : "transparent",
              color: filter === key ? val.color : "#64748b",
              fontSize: 11,
              fontWeight: 700,
              cursor: "pointer",
              whiteSpace: "nowrap",
            }}
          >
            {val.label}
          </button>
        ))}
      </div>

      {/* Stats Bar */}
      <div style={{
        display: "flex",
        gap: 0,
        background: "#0a0814",
        borderBottom: "1px solid #ffffff08",
        padding: "10px 16px",
        overflowX: "auto",
      }}>
        {Object.entries(CONTENT_TYPES).map(([key, val]) => {
          const count = days.filter(d => d.type === key).length;
          return (
            <div key={key} style={{ textAlign: "center", flex: "0 0 auto", padding: "0 12px" }}>
              <div style={{ fontSize: 16, fontWeight: 800, color: val.color }}>{count}</div>
              <div style={{ fontSize: 9, color: "#475569", letterSpacing: 0.5 }}>{key}</div>
            </div>
          );
        })}
      </div>

      {/* Calendar Grid */}
      <div style={{ padding: "16px 16px 120px" }}>
        {filter === "ALL" ? (
          [1, 2, 3, 4, 5].map(week => {
            const weekDays = days.filter(d => getWeek(d.day) === week);
            if (weekDays.length === 0) return null;
            return (
              <div key={week} style={{ marginBottom: 24 }}>
                <div style={{
                  fontSize: 10,
                  fontWeight: 800,
                  color: "#4a5568",
                  letterSpacing: 3,
                  textTransform: "uppercase",
                  marginBottom: 10,
                  paddingLeft: 4,
                }}>
                  {weekLabels[week - 1]}
                </div>
                <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 10 }}>
                  {weekDays.map(d => <DayCard key={d.day} d={d} onClick={() => setSelected(d)} />)}
                </div>
              </div>
            );
          })
        ) : (
          <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 10 }}>
            {filtered.map(d => <DayCard key={d.day} d={d} onClick={() => setSelected(d)} />)}
          </div>
        )}
      </div>

      {/* Detail Modal */}
      {selected && (
        <div
          style={{
            position: "fixed", inset: 0,
            background: "#000000cc",
            zIndex: 100,
            display: "flex",
            alignItems: "flex-end",
            backdropFilter: "blur(4px)",
          }}
          onClick={() => setSelected(null)}
        >
          <div
            style={{
              background: "#111020",
              border: "1px solid #ffffff12",
              borderRadius: "24px 24px 0 0",
              padding: "24px 20px 40px",
              width: "100%",
              maxHeight: "85vh",
              overflowY: "auto",
            }}
            onClick={e => e.stopPropagation()}
          >
            {/* Modal Header */}
            <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start", marginBottom: 16 }}>
              <div>
                <div style={{ display: "flex", alignItems: "center", gap: 8, marginBottom: 6 }}>
                  <span style={{
                    padding: "3px 10px",
                    borderRadius: 12,
                    background: CONTENT_TYPES[selected.type].bg,
                    color: CONTENT_TYPES[selected.type].color,
                    fontSize: 11,
                    fontWeight: 700,
                  }}>
                    {CONTENT_TYPES[selected.type].label}
                  </span>
                  <span style={{ fontSize: 11, color: "#475569" }}>Day {selected.day}</span>
                </div>
                <h3 style={{ fontSize: 17, fontWeight: 800, margin: 0, color: "#fff" }}>
                  {selected.title}
                </h3>
              </div>
              <button
                onClick={() => setSelected(null)}
                style={{
                  background: "#ffffff10",
                  border: "none",
                  borderRadius: 10,
                  color: "#94a3b8",
                  width: 32,
                  height: 32,
                  cursor: "pointer",
                  fontSize: 16,
                  display: "flex",
                  alignItems: "center",
                  justifyContent: "center",
                  flexShrink: 0,
                }}
              >
                ✕
              </button>
            </div>

            {/* Hook */}
            <div style={{
              background: `${CONTENT_TYPES[selected.type].color}12`,
              border: `1px solid ${CONTENT_TYPES[selected.type].color}30`,
              borderRadius: 12,
              padding: "10px 14px",
              marginBottom: 14,
            }}>
              <div style={{ fontSize: 10, color: CONTENT_TYPES[selected.type].color, fontWeight: 700, letterSpacing: 1, marginBottom: 4 }}>
                ⚡ WHY THIS WORKS
              </div>
              <div style={{ fontSize: 12, color: "#cbd5e1", lineHeight: 1.6 }}>{selected.hook}</div>
            </div>

            {/* Visual Direction */}
            <div style={{
              background: "#ffffff06",
              border: "1px solid #ffffff10",
              borderRadius: 12,
              padding: "10px 14px",
              marginBottom: 14,
            }}>
              <div style={{ fontSize: 10, color: "#6366f1", fontWeight: 700, letterSpacing: 1, marginBottom: 4 }}>
                🎥 VISUAL DIRECTION
              </div>
              <div style={{ fontSize: 12, color: "#94a3b8", lineHeight: 1.6 }}>{selected.visual}</div>
            </div>

            {/* Caption */}
            <div style={{
              background: "#ffffff06",
              border: "1px solid #ffffff10",
              borderRadius: 12,
              padding: "12px 14px",
              marginBottom: 12,
            }}>
              <div style={{ fontSize: 10, color: "#10b981", fontWeight: 700, letterSpacing: 1, marginBottom: 8 }}>
                📝 CAPTION
              </div>
              <div style={{
                fontSize: 12,
                color: "#e2e8f0",
                lineHeight: 1.8,
                whiteSpace: "pre-line",
                fontFamily: "monospace",
              }}>
                {selected.caption}
              </div>
            </div>

            {/* CTA */}
            <div style={{
              background: "#f59e0b12",
              border: "1px solid #f59e0b30",
              borderRadius: 12,
              padding: "10px 14px",
              marginBottom: 16,
            }}>
              <div style={{ fontSize: 10, color: "#f59e0b", fontWeight: 700, letterSpacing: 1, marginBottom: 4 }}>
                📣 CALL TO ACTION
              </div>
              <div style={{ fontSize: 12, color: "#fcd34d", lineHeight: 1.6 }}>{selected.cta}</div>
            </div>

            {/* Copy Button */}
            <button
              onClick={() => handleCopy(selected.caption)}
              style={{
                width: "100%",
                padding: "14px",
                background: copied ? "#10b981" : `linear-gradient(135deg, ${CONTENT_TYPES[selected.type].color}, #a855f7)`,
                border: "none",
                borderRadius: 14,
                color: "#fff",
                fontSize: 14,
                fontWeight: 800,
                cursor: "pointer",
                letterSpacing: 0.5,
                transition: "all 0.2s",
              }}
            >
              {copied ? "✅ Copied to Clipboard!" : "📋 Copy Caption"}
            </button>
          </div>
        </div>
      )}
    </div>
  );
}

function DayCard({ d, onClick }) {
  const type = CONTENT_TYPES[d.type];
  return (
    <div
      onClick={onClick}
      style={{
        background: "#0f0d1c",
        border: `1px solid ${type.color}25`,
        borderRadius: 16,
        padding: "14px 12px",
        cursor: "pointer",
        transition: "all 0.2s",
        position: "relative",
        overflow: "hidden",
      }}
    >
      <div style={{
        position: "absolute",
        top: 0, right: 0,
        width: 60, height: 60,
        background: `${type.color}08`,
        borderRadius: "0 16px 0 60px",
      }} />
      <div style={{
        fontSize: 9,
        fontWeight: 800,
        color: type.color,
        letterSpacing: 1,
        marginBottom: 6,
        textTransform: "uppercase",
      }}>
        Day {d.day}
      </div>
      <div style={{
        display: "inline-block",
        padding: "2px 8px",
        borderRadius: 8,
        background: type.bg,
        color: type.color,
        fontSize: 9,
        fontWeight: 700,
        marginBottom: 8,
      }}>
        {type.label}
      </div>
      <div style={{
        fontSize: 12,
        fontWeight: 700,
        color: "#e2e8f0",
        lineHeight: 1.4,
        marginBottom: 8,
      }}>
        {d.title}
      </div>
      <div style={{
        fontSize: 10,
        color: "#475569",
        lineHeight: 1.5,
        overflow: "hidden",
        display: "-webkit-box",
        WebkitLineClamp: 2,
        WebkitBoxOrient: "vertical",
      }}>
        {d.caption.split("\n")[0]}
      </div>
      <div style={{
        marginTop: 10,
        fontSize: 9,
        color: type.color,
        fontWeight: 700,
        letterSpacing: 0.5,
      }}>
        Tap for full details →
      </div>
    </div>
  );
}
