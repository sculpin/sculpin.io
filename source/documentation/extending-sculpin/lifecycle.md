---
title: Sculpin Lifecycle
slug: extending-sculpin/lifecycle

---

The following represents the lifecycle of a single pass through all of the
sources.

 * Generate (Generators)
 * Permalink Creation
 * Convert
 * Format
 * Output

For a single "run" (think `sculpin generate`) there is only one run and every
source is considered dirty and needs to be written.

For multiple "runs" (think `sculpin generate --watch`) there are many runs. For
the first "run", every source is considered dirty and needs to be written. After
that, each additional "run" will determine whether or not a source is dirty
based on whether it has been updated since the previous run.

### Events

 * **Sculpin\Core\Sculpin::EVENT_BEFORE_RUN**
   Called very early in the run lifecycle. Suitable for setting up sources
   before anything else is done. Is passed a `SourceSetEvent` instance.
 * **Sculpin\Core\Sculpin::EVENT_BEFORE_CONVERT**
   Called just before a source is converted. Suitable for massaging a source
   prior to conversion. Passed a `ConvertEvent` instance.
 * **Sculpin\Core\Sculpin::EVENT_AFTER_CONVERT**
   Called just after a source is converted. Suitable for massaging a source
   after conversion. Passed a `ConvertEvent` instance.
 * **Sculpin\Core\Sculpin::EVENT_BEFORE_FORMAT**
   Called just before a source is formatted. Passed a `FormatEvent` instance.
 * **Sculpin\Core\Sculpin::EVENT_AFTER_FORMAT**
   Called just after a source is formatted. Passed a `SourceSetEvent` instance.
 * **Sculpin\Core\Sculpin::EVENT_AFTER_RUN**
   Called very late into the run lifecycle. Suitable for cleanup. Is passed a
   `SourceSetEvent` instance.
