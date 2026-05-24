import React, { useMemo, useState } from "react";

const DOCUMENTS = [
  {
    name: "Delmar Yesaya Junior Cime Tanihaha",
    url: "https://docs.google.com/document/d/1FfvpHftdjnWNjWC9tQ1Z_1TW5Te-LaNrysVYCZHfzrM/edit?usp=sharing",
  },
  {
    name: "Theodore Diago Wijaya",
    url: "https://docs.google.com/document/d/1vZfHoze0XC9iqur6deInjDAmoEwab4cIZ-zMZfkbHtw/edit?usp=drive_link",
  },
  {
    name: "Nadya Shakira Febriani",
    url: "https://docs.google.com/document/d/1IZ-eHQ4XieMJmVhf0D8TmOsGy69lM6eh1Zk91g3QO4g/edit?usp=drive_link",
  },
  {
    name: "Miranda Alvina Trilaras",
    url: "https://docs.google.com/document/d/1nEzWmaOjYo35FxhtRFa0SQcp65IBcUNXd3yh6xtdsAE/edit?usp=drive_link",
  },
  {
    name: "Gerald Austin Limena",
    url: "https://docs.google.com/document/d/1mmbbCkXOjdudrY0h7xXUs7ceoul_AgKCNJKfKvipSRY/edit?usp=drive_link",
  },
  {
    name: "Darren Cristian Jomi",
    url: "https://docs.google.com/document/d/1Ubqg7xOxkLOH6UqcxrIcUxfjx_JbXS_COg2IsyuTSU4/edit?usp=drive_link",
  },
  {
    name: "Joanna Lee",
    url: "https://docs.google.com/document/d/1UOzifL42SrQiTpG-X3scATqlNQwE95mZOFV1KP_7dWQ/edit?usp=drive_link",
  },
  {
    name: "Jason Nathaniel Soesanto",
    url: "https://docs.google.com/document/d/1wzK18rlvWmu7fNDKKlpQ9QD-PgZ9yB47ukraOZFVUqo/edit?usp=drive_link",
  },
  {
    name: "Geoffrey Aaron Bennet",
    url: "https://docs.google.com/document/d/13klYq4oxIuWfcMKwl4HdqG5GPumZwJDCwyWbJl4T2bg/edit?usp=drive_link",
  },
  {
    name: "Andersen Sidik Djojowahono",
    url: "https://docs.google.com/document/d/1JmFhADkibryoKPo7TMUd1iBo4vj0ggoS2Wrm0kjNLnU/edit?usp=drive_link",
  },
  {
    name: "Poh Priscilla Eugene Dharma Saputra",
    url: "https://docs.google.com/document/d/1OPiE2lpCJyPtreoeFsnzpMFYzIKahNhTzJcTIA1jvHQ/edit?usp=drive_link",
  },
];

function normalizeText(value) {
  return value.toLowerCase().trim().split(/\s+/).filter(Boolean).join(" ");
}

function toPreviewUrl(url) {
  return url.includes("/edit") ? url.replace("/edit", "/preview") : url;
}

export default function NameToDocLookupWebsite() {
  const [name, setName] = useState("");
  const [unlockedDoc, setUnlockedDoc] = useState(null);

  const matchedDoc = useMemo(() => {
    const query = normalizeText(name);
    if (!query) return null;
    return DOCUMENTS.find((doc) => normalizeText(doc.name) === query) || null;
  }, [name]);

  const handleEnter = () => {
    setUnlockedDoc(matchedDoc);
  };

  return (
    <div className="min-h-screen bg-[radial-gradient(circle_at_top,_rgba(255,247,237,0.14)_0%,_rgba(15,23,42,0.96)_40%,_rgba(2,6,23,1)_100%)] text-slate-900">
      <div className="mx-auto flex min-h-screen max-w-4xl items-center justify-center px-4 py-10 sm:px-6">
        {!unlockedDoc ? (
          <div className="w-full max-w-md rounded-[2rem] border border-white/10 bg-white/90 p-8 shadow-2xl shadow-black/35 backdrop-blur-xl sm:p-10">
            <div className="text-center">
              <h1 className="text-3xl font-semibold tracking-tight text-slate-900 sm:text-4xl">
                Enter Full Name
              </h1>
            </div>

            <div className="mt-8 rounded-2xl border border-slate-200 bg-[#fbf7ef] p-3 shadow-inner">
              <input
                type="text"
                value={name}
                onChange={(e) => {
                  setName(e.target.value);
                  setUnlockedDoc(null);
                }}
                onKeyDown={(e) => {
                  if (e.key === "Enter") handleEnter();
                }}
                placeholder="Enter Full Name"
                autoComplete="off"
                spellCheck="false"
                className="w-full rounded-xl border-0 bg-transparent px-3 py-3 text-base text-slate-900 outline-none placeholder:text-slate-400"
              />
            </div>

            <button
              onClick={handleEnter}
              className="mt-5 w-full rounded-2xl bg-slate-900 px-4 py-3 font-medium text-white transition hover:bg-slate-800"
            >
              Enter
            </button>
          </div>
        ) : (
          <div className="w-full max-w-4xl rounded-[2rem] border border-white/10 bg-[#fbf7ef] p-5 text-slate-900 shadow-2xl shadow-black/35 sm:p-8">
            <div className="mx-auto max-w-3xl">
              <div className="border-b border-slate-300/70 pb-5 text-center">
                <div className="text-xs uppercase tracking-[0.35em] text-slate-500">
                  A Letter For
                </div>
                <h1 className="mt-3 font-serif text-3xl font-semibold tracking-tight sm:text-4xl">
                  {unlockedDoc.name}
                </h1>
              </div>

              <div className="mt-6 rounded-2xl bg-white/70 p-5 sm:p-8">
                <p className="font-serif text-lg leading-8 text-slate-800 sm:text-xl">
                  Your letter is ready. Open it below, or view the preview in this page.
                </p>

                <div className="mt-8 flex flex-wrap gap-3">
                  <a
                    href={unlockedDoc.url}
                    target="_blank"
                    rel="noreferrer"
                    className="rounded-full bg-slate-900 px-5 py-3 text-sm font-medium text-white transition hover:bg-slate-800"
                  >
                    Open document
                  </a>
                  <button
                    onClick={() => {
                      setUnlockedDoc(null);
                      setName("");
                    }}
                    className="rounded-full border border-slate-300 bg-transparent px-5 py-3 text-sm font-medium text-slate-700 transition hover:bg-slate-100"
                  >
                    Back
                  </button>
                </div>
              </div>

              <div className="mt-6 overflow-hidden rounded-2xl border border-slate-300 bg-white shadow-lg">
                <iframe
                  title="Document Preview"
                  src={toPreviewUrl(unlockedDoc.url)}
                  className="h-[72vh] w-full"
                />
              </div>
            </div>
          </div>
        )}
      </div>
    </div>
  );
}
